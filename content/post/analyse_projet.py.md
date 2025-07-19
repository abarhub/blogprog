+++
title = "Analyse une liste de projets"
date = "2024-09-29"
description = "Analyse une liste de projets"
tags = ["python"]
summary = "Analyse une liste de projets"
+++
import json
import os
import subprocess
import sys
import xml.etree.ElementTree as ET
from datetime import date, datetime
import time

from boltons.iterutils import remap

'''

jq . projet_240928_182342.json

jq .[].nom projet_240928_182342.json

jq .[].nom,.[].modules[].name projet_240928_182342.json

jq "[ .[] | {nom_module: .modules[].name} ]" projet_240928_182342.json

jq "[ .[] | . as $parent | {nom_module: .modules[].name, projet: $parent.nom} ]" projet_240928_182342.json

Pour lister le nom des produits :
jq "[ .[] | . as $parent | {nom_module: .modules[].name, projet: $parent.nom} ]" projet_240929_131613.json

Pour lister la version d'angular :
jq "[ .[] | . as $parent | {nom_module: .modules[].name, projet: $parent.nom, angular: .modules[].packageJson.dependencies.\"@angular/core\"} ]" projet_240929_131613.json

Pour lister la version de java :
jq "[ .[] | . as $parent | {nom_module: .modules[].name, projet: $parent.nom, java: .modules[].pom.properties.\"java.version\"} ]" projet_240929_131613.json

Pour lister la version du projet :
jq "[ .[] | . as $parent | {nom_module: .modules[].name, projet: $parent.nom, version_projet: .modules[].pom.effectivePom.version.version} ]" projet_240929_131613.json

Pour lister le groupId, l'artifactId et la version des projets :
jq "[ .[] | . as $parent | {nom_module: .modules[].name, projet: $parent.nom, version_projet: ( .modules[].pom.effectivePom.version.groupId + \":\" + .modules[].pom.effectivePom.version.artifactId + \":\" + .modules[].pom.effectivePom.version.version ) } ]" projet_240929_131613.json

'''


class Parametres:

    def __init__(self):
        self.repertoires = []
        self.repertoires_ignore = []
        self.debug = False


class ErreurRunMvnException(Exception):
    pass


class ErreurRunGitException(Exception):
    pass


def is_git_repo(path):
    """Vérifie si un répertoire est un repo git."""
    return os.path.isdir(os.path.join(path, ".git"))


def parse_pom(pom_path):
    tree = ET.parse(pom_path)
    root = tree.getroot()

    # Espaces de noms (pour éviter les erreurs lors de la recherche d'éléments dans le fichier XML)
    namespaces = {'maven': 'http://maven.apache.org/POM/4.0.0'}

    # Récupérer les informations du parent s'il existe
    parent = root.find('maven:parent', namespaces)
    parent_info = {}
    if parent is not None:
        if parent.find('maven:groupId', namespaces) is not None:
            parent_info['groupId'] = parent.find('maven:groupId', namespaces).text
        if parent.find('maven:artifactId', namespaces) is not None:
            parent_info['artifactId'] = parent.find('maven:artifactId', namespaces).text
        if parent.find('maven:version', namespaces) is not None:
            parent_info['version'] = parent.find('maven:version', namespaces).text

    version_projet = {}
    root.find('maven:parent', namespaces)
    if root.find('maven:groupId', namespaces) is not None:
        version_projet['groupId'] = root.find('maven:groupId', namespaces).text
    if root.find('maven:artifactId', namespaces) is not None:
        version_projet['artifactId'] = root.find('maven:artifactId', namespaces).text
    if root.find('maven:version', namespaces) is not None:
        version_projet['version'] = root.find('maven:version', namespaces).text

    # Récupérer les propriétés s'il existe
    properties = root.find('maven:properties', namespaces)
    props = {}
    if properties is not None:
        for prop in properties:
            props[prop.tag.split('}')[-1]] = prop.text

    return parent_info, props, version_projet


def parse_pom_xml(pom_path, debug):
    """Parse le fichier pom.xml et extrait les informations du parent et des propriétés."""

    parent_info, props, version_projet = parse_pom(pom_path)

    # les dépendances
    dependances = None
    effectivePom = None
    try:
        currentDir = os.getcwd()
        outpoutFile = f'{currentDir}/data/dependency.json'
        command = f"mvn dependency:3.8.0:tree -DoutputType=json -DoutputFile={currentDir}/data/dependency.json -DoutputEncoding=utf8"
        repo_path = os.path.dirname(pom_path)
        result = subprocess.run(command, cwd=repo_path, shell=True, capture_output=True, text=True)
        if debug or result.returncode != 0:
            print("dependancy tree output:" + result.stdout)
            print("dependancy tree error:" + result.stderr)
        if result.returncode != 0:
            raise ErreurRunMvnException(f"Erreur lors de l'exécution de la commande {command}: {result.stderr}")
        if os.path.isfile(outpoutFile):
            with open(outpoutFile, 'r', encoding='utf-8') as file:
                data = json.load(file)
                if data is not None:
                    bad_keys = {'classifier', 'type', 'classifier', 'optional'}

                    drop_keys = lambda path, key, value: key not in bad_keys
                    clean = remap(data, visit=drop_keys)
                    if clean is not None:
                        dependances = clean

        # analyse effective pom
        outpoutFile = f'{currentDir}/data/effectivePom.xml'
        command = f"mvn help:effective-pom -Doutput={outpoutFile}"
        repo_path = os.path.dirname(pom_path)
        result = subprocess.run(command, cwd=repo_path, shell=True, capture_output=True, text=True)
        if debug or result.returncode != 0:
            print("effective-pom output:" + result.stdout)
            print("effective-pom error:" + result.stderr)
        if result.returncode != 0:
            raise ErreurRunMvnException(f"Erreur lors de l'exécution de la commande {command}: {result.stderr}")
        if os.path.isfile(outpoutFile):
            parent_info_effective, props_effective, version_projet_effective = parse_pom(outpoutFile)

            if parent_info_effective is not None or props_effective is not None or version_projet_effective is not None:
                effectivePom = {}
                if parent_info_effective is not None:
                    effectivePom['parent_info'] = parent_info_effective
                if version_projet_effective is not None:
                    effectivePom['version'] = version_projet_effective
                if props_effective is not None:
                    effectivePom['properties'] = props_effective
    except ErreurRunMvnException as e:
        details = e.args[0]
        print(f"Erreur pour analyser le pom {pom_path} : {details}")

    return parent_info, props, version_projet, dependances, effectivePom


def parse_package_json(package_path):
    """Parse le fichier package.json et extrait la version d'Angular/CLI s'il existe."""
    mapVersion = {}
    with open(package_path, 'r', encoding='utf-8') as file:
        data = json.load(file)
        dependencies = data.get('dependencies', {})
        devDependencies = data.get('devDependencies', {})
        if dependencies is not None:
            mapVersion['dependencies'] = dependencies
        if devDependencies is not None:
            mapVersion['devDependencies'] = devDependencies
        name = data.get('name', {})
        if name is not None:
            mapVersion['name'] = name
        version = data.get('version', {})
        if version is not None:
            mapVersion['version'] = version
        scripts = data.get('scripts', {})
        if scripts is not None:
            mapVersion['scripts'] = scripts

    return mapVersion


def run_git_command(command, repo_path):
    """Exécute une commande git et retourne la sortie."""
    result = subprocess.run(command, cwd=repo_path, shell=True, capture_output=True, text=True)
    if result.returncode != 0:
        raise ErreurRunGitException(f"Erreur lors de l'exécution de la commande {command}: {result.stderr}")
    return result.stdout


def get_branch_info(branch):
    """Extrait les informations d'une branche (nom, date, hash court, message de commit)."""
    parts = branch.split(maxsplit=5)
    short_commit = parts[0]
    date_str = parts[1] + " " + parts[2] + " " + parts[3] if len(parts) > 3 else ""
    # print(f"{short_commit}: {date_str}!{parts}")
    date = datetime.strptime(date_str, "%Y-%m-%d %H:%M:%S %z") if len(date_str) > 0 else None
    name = parts[4] if len(parts) > 3 else ""
    message = parts[5] if len(parts) > 4 else ""
    return short_commit, date, message, name


def has_uncommitted_changes(repo_path):
    """Vérifie s'il y a des fichiers non commités dans le dépôt."""
    status_output = run_git_command("git status --porcelain", repo_path)
    if status_output.strip():  # Si la sortie n'est pas vide, il y a des changements non commités
        return True
    return False


def get_local_branche(repo_path) -> str:
    """Vérifie s'il y a des fichiers non commités dans le dépôt."""
    status_output = run_git_command("git rev-parse --abbrev-ref HEAD", repo_path)
    res = status_output.strip()
    if res:  # Si la sortie n'est pas vide, il y a des changements non commités
        return res
    return None


def fetch_and_list_branches(repo_path):
    # Étape 1: Faire un git fetch
    try:
        run_git_command("git fetch --all", repo_path)
    except ErreurRunGitException as e:
        details = e.args[0]
        print(f"Erreur pour executer git {repo_path} : {details}")
        return None, None, None, None

    localBranche = get_local_branche(repo_path)

    # Étape 3: Obtenir les 5 dernières branches distantes
    remote_branches_output = run_git_command(
        "git for-each-ref --sort=-committerdate --format=\"%(objectname:short) %(committerdate:iso8601) %(refname:short) %(contents:subject)\" refs/remotes --count=5",
        repo_path
    )
    remote_branches = []
    # list_remote_branche=[]
    for line in remote_branches_output.strip().split("\n"):
        if line:
            short_commit, date, message, nameBranche2 = get_branch_info(line)
            liste = line.split()
            if len(liste) >= 2:
                branch_name = nameBranche2  # liste[2]
                remote_branches.append({
                    "name": branch_name,
                    "commit": short_commit,
                    "date": date.isoformat(),
                    "message": message
                })
                # list_remote_branche.append(branch_name)

    # Étape 2: Obtenir les 5 dernières branches locales
    local_branches_output = run_git_command(
        "git for-each-ref --sort=-committerdate --format=\"%(objectname:short) %(committerdate:iso8601) %(refname:short) %(contents:subject)\" refs/heads --count=5",
        repo_path
    )
    # print(local_branches_output)
    local_branches = []
    for line in local_branches_output.strip().split("\n"):
        if line:
            # print(f'line: {line}')
            short_commit, date, message, nameBranche = get_branch_info(line)
            liste = line.split()
            if len(liste) >= 2:
                branch_name = nameBranche  # liste[2]
                branche_module = {
                    "name": branch_name,
                    "commit": short_commit,
                    "date": date.isoformat(),
                    "message": message
                }
                local_branches.append(branche_module)
                if localBranche is not None and localBranche == branch_name:
                    branche_module["current"] = True
                liste_remote = [item for item in remote_branches if item["name"] == "origin/" + branch_name]
                if liste_remote:
                    branche_module["remote_exists"] = True
                    branche_module["remote_eq"] = liste_remote[0]['commit'] == short_commit
                else:
                    branche_module["remote_exists"] = False

    fichierNonCommite = has_uncommitted_changes(repo_path)

    # Étape 4: Retourner un objet structuré avec les branches locales et distantes
    return local_branches, remote_branches, fichierNonCommite, localBranche


def find_repos_and_parse_files(parametre: Parametres):
    """Cherche dans les sous-répertoires pour identifier les repos git ou ceux contenant pom.xml ou package.json."""

    # start_dir_list, debug, ignoreProjet
    listeGlobal = []
    # nomFichierGlobal=f"{start_dir}/.git"

    today = datetime.today()
    filename = today.strftime("projet_%y%m%d_%H%M%S.json")

    for start_dir in parametre.repertoires:
        for root, dirs, files in os.walk(start_dir):
            if is_git_repo(root) or "pom.xml" in files or "package.json" in files:
                # print(f"\nDépôt Git trouvé dans : {root}")

                pathFile = os.path.basename(root)

                dirs[:] = []

                if parametre.repertoires_ignore is not None and pathFile in parametre.repertoires_ignore:
                    print(f"projet ignore {pathFile} : {root}")
                    continue

                print(f"projet {pathFile} : {root}")
                projet = {
                    'nom': pathFile,
                    'rep': root,
                    'modules': []
                }
                listeGlobal.append(projet)
                root0 = root

                for root2, dirs2, files2 in os.walk(root0):

                    depotGit = is_git_repo(root2)

                    dirs2[:] = [d for d in dirs2 if d not in {'node', 'node_modules', 'target', '.venv', '.git'}]

                    if "pom.xml" in files2 or "package.json" in files2:
                        # print(f"\nProjet : {root}")
                        liste = []
                        name = '.'
                        if root2 != root0:
                            name = os.path.basename(root2)
                        module = {
                            'name': name,
                            'path': root2
                        }
                        projet['modules'].append(module)

                        if "pom.xml" in files2:
                            pom_path = os.path.join(root2, "pom.xml")
                            parent_info, properties, version_projet, dependances, effectivePom = parse_pom_xml(pom_path,
                                                                                                               parametre.debug)
                            pom = {
                            }
                            if parent_info is not None:
                                pom['parent_info'] = parent_info
                            if version_projet is not None:
                                pom['version'] = version_projet
                            if properties is not None:
                                pom['properties'] = properties
                            if dependances is not None:
                                pom['dependances'] = dependances
                            if effectivePom is not None:
                                pom['effectivePom'] = effectivePom
                            module['pom'] = pom
                        if "package.json" in files2:
                            package_path = os.path.join(root2, "package.json")
                            map = parse_package_json(package_path)
                            if map is not None:
                                module['packageJson'] = map

                        if depotGit:
                            local_branches, remote_branches, fichierNonCommite, localBranche = fetch_and_list_branches(
                                root2)
                            gitModule = {
                                'localBranches': local_branches,
                                'remoteBranches': remote_branches,
                                'fichierNonCommite': fichierNonCommite,
                                'localBranche': localBranche
                            }
                            module['git'] = gitModule

    with open(f"data/{filename}", "w") as outfile:
        json.dump(listeGlobal, outfile)


print("date de debut : " + datetime.now().strftime("%Y-%m-%d %H:%M:%S"))
start = datetime.now()

param = sys.argv

parametres = Parametres()

debut_parametre = '--parametre='
debut_ignore = '--ignore='
debut_debug = '--debug'

for p in param[1:]:
    if p.startswith(debut_parametre):
        s = p[len(debut_parametre):]
        parametres.repertoires = s.split(',')
    elif p.startswith(debut_ignore):
        s = p[len(debut_ignore):]
        parametres.repertoires_ignore = s.split(',')
    elif p == debut_debug:
        parametres.debug = True
    else:
        raise Exception("Parametre invalide : " + p)

if not parametres.repertoires:
    raise Exception("Liste des répertoires absente")

find_repos_and_parse_files(parametres)

print("date de fin : " + datetime.now().strftime("%Y-%m-%d %H:%M:%S"))
delta = datetime.now() - start
ms = delta.total_seconds() * 1000
milli = int(ms % 1000)
seconds = (ms / 1000) % 60
seconds = int(seconds)
minutes = (ms / (1000 * 60)) % 60
minutes = int(minutes)
hours = int(ms / (1000 * 60 * 60)) % 24
print(f"duree d'execution : {hours:02d}:{minutes:02d}:{seconds:02d}.{milli:03d} ({ms} ms)")

                    
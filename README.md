# blogprog
Blog de programmation créé avec [Hugo](https://gohugo.io/)

Le site a été généré par l'outils [Hugo](https://gohugo.io/) en version 0.93.0 extended et le template [fuji](https://github.com/dsrkafuu/hugo-theme-fuji/)

Pour démarrer le serveur pour le dev :
```shell
hugo server -D
```

Pour générer les pages :
```shell
hugo -D
```
Les fichiers sont générés dans le répertoire docs/. Il faut penser à supprimer le contenu avant de lancer la génération.


Le site généré est [ici](https://abarhub.github.io/blogprog/).

Pour le mettre àjour, il faut executer l'outils updatesite.

# hugoBasicExample

This repository offers an example site for [Hugo](https://gohugo.io/) and also it provides the default content for demos hosted on the [Hugo Themes Showcase](https://themes.gohugo.io/).

# Using

1. [Install Hugo](https://gohugo.io/overview/installing/)
2. Clone this repository
```bash
git clone https://github.com/gohugoio/hugoBasicExample.git
cd hugoBasicExample
```
3. Clone the repository you want to test. If you want to test all Hugo Themes then follow the instructions provided [here](https://github.com/gohugoio/hugoThemes#installing-all-themes)
4. Run Hugo and select the theme of your choosing
```bash
hugo server -t YOURTHEME
```
5. Under `/content/` this repository contains the following:
- A section called `/post/` with sample markdown content
- A headless bundle called `homepage` that you may want to use for single page applications. You can find instructions about headless bundles over [here](https://gohugo.io/content-management/page-bundles/#headless-bundle)
- An `about.md` that is intended to provide the `/about/` page for a theme demo
6. If you intend to build a theme that does not fit in the content structure provided in this repository, then you are still more than welcome to submit it for review at the [Hugo Themes](https://github.com/gohugoio/hugoThemes/issues) repository


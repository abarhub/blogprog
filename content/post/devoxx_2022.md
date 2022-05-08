+++
title = "Devoxx 2022"
date = "2022-04-23"
description = "Devoxx 2022 du 20 au 22 avril "
tags = ["devoxx"]
summary = "Devoxx 2022 du 20 au 22 avril "
+++

# Devoxx 2022 du 20 au 22 avril

## Mercredi 20 avril

[Programme](https://cfp.devoxx.fr/2022/byday/wed)
[Videos](https://www.youtube.com/c/DevoxxFRvideos/featured)

### [Spring Security - décodage et démystification](https://cfp.devoxx.fr/2022/talk/UBP-3035/Spring_Security_-_decodage_et_demystification_%F0%9F%95%B5%EF%B8%8F)
* Il faut mieux créer un bean plutot que de dériver de WebSecurityConfiguration
* Il est possible d'ajouter une methode dans la configuration du http
* Pour débuger, on peut augmenter le niveau de log ou mettre des points d'arret pour débuger

[Video](https://www.youtube.com/watch?v=wYR6L_1Jb4I)

### [Loom nous Protègera-t-il du Braquage Temporel ?](https://cfp.devoxx.fr/2022/talk/IFY-4656/Loom_nous_Protegera-t-il_du_Braquage_Temporel_%3F)
C'est des taches qui ne sont pas des vrai thread. 
On peut en créer des millions sans problème, et sans utiliser 2Mo de stack par thread.
Par contre cela pose problème si dans le code il y a des accès IO ou avec du code C.
Ne sera pas pret avant Java 20 au moins.

[Vidéo](https://www.youtube.com/watch?v=wx7t69DylsI)

### [Gitpod: la fin des frictions inutiles pour contribuer à un projet OSS ?](https://cfp.devoxx.fr/2022/talk/SKW-4406/Gitpod:_la_fin_des_frictions_inutiles_pour_contribuer_a_un_projet_OSS_%3F)
L'idée, c'est de créer un contener distant qui peut être utiliser pour travailler avec un environnement pret à être utilisé.
La version gratuite permet d'utiliser 50 heure par mois. 
Il faut penser à fermer la session pour ne pas utiliser inutilement des ressources.

[Vidéo](https://www.youtube.com/watch?v=7OlynADvoCc)

### [Bien maîtriser les Dev Tools de vos navigateurs](https://cfp.devoxx.fr/2022/talk/IKR-5883/Bien_maitriser_les_Dev_Tools_de_vos_navigateurs)
Il y a l'outils Lighthouse qui permet en un clique de savoir s'il y a des problèmes dans la page, et si elle est mal conçu.
Voir les recommendations d'accessibilité de chrome (il existe une norme).
Afficher l'ordre des composants pour voir s'il est correcte et s'il existe.
Voir le temps de chargement des pages.
Modifier les elements flex.
Enregistrer les modification pour les garder quand la page est rechargée.
Enregistrer les actions et les rejouer.

[Vidéo](https://www.youtube.com/watch?v=TVJhAda0Ex0)

### [Construisons ensemble une application Micro-Frontend multi-frameworks avec Webpack 5 Module Federation](https://cfp.devoxx.fr/2022/talk/TPG-0599/Construisons_ensemble_une_application_Micro-Frontend_multi-frameworks_avec_Webpack_5_Module_Federation)
Ca a l'air assez simple de le mettre en place. Il faut voir la vidéo pour voir comment faire.

[Vidéo](https://www.youtube.com/watch?v=zOU8wTCx8io)

## Jeudi 21 avril

[Programme](https://cfp.devoxx.fr/2022/byday/thu)

### [OAUTH 2.1 expliqué simplement (même si tu n'es pas dev) !](https://cfp.devoxx.fr/2022/talk/YHH-6414/OAUTH_2.1_explique_simplement_(meme_si_tu_n'es_pas_dev)_!)
Il y a peut de différence entre OAuth 2.0 et OAuth 2.1.
* Il faut mettre l'url complete pour la page de redirection
* Il faut utiliser implicite flow avec PKCE

[Vidéo](https://www.youtube.com/watch?v=YdShQveywpo)

### [Le (dés)amour des tests web](https://cfp.devoxx.fr/2022/talk/QUS-1105/Le_(des)amour_des_tests_web)
Le property based testing permet de tester des cas complexe (problème de latence)
Il faut mocker les appels distants. Il y a un librairie qui permet de faire ça bien.
Il faut essayer de faire des tests indépendant de l'odre d'affichage.
Il faut que les tests soit rapides, sinon ils ne seront pas lancées.
Si le propertie based testing trouve un bug interressant, il faut mieux faire un testpour ce cas.
Il n'est pas conseillé de faire la pyramide de test pour les tests du front.
Pour les TU, il ne doit pas y en avoir trop. Il faut mieux se concentrer soit sur les tests d'intégrations, soit les tests fonctionnelles.
Voir [fast-check](https://github.com/dubzzz/fast-check) pour faire des tests web. Voir la video vers 27min pour des tests property based testing sur les traitements concurents et détecter les races conditions.

[Vidéo](https://www.youtube.com/watch?v=stUvCpRk7vo)

### [Fuzzing en Go](https://cfp.devoxx.fr/2022/talk/VHP-9005/Fuzzing_en_Go)
Le fussing est une nouvauté de golang 1.18; Il est fait en prenant en compte la structure du code, c-a-d qu'il va essayer de parcourir toutes les branches.
Il permet de détecter les problèmes de sécurités.

[Vidéo](https://www.youtube.com/watch?v=Oyjo0krQz5M)

### [What's cooking in Maven?](https://cfp.devoxx.fr/2022/talk/MPH-2660/What's_cooking_in_Maven%3F)
* Les maven warpeur permet de gérer la version au niveau du projet. Cela fixe la version de maven. par contre, les dépendances maven (jar) sont aussi dans le répertoire du projet. Cela fonctionne déja en maven 3.x
* Build/Consum POM permet de mettre à jour la version du pom au moment du déploiement. Cela permet que si un projet a la version que dans le pom du parent, au moment du deploiement la version est ajouté dans le pom enfant, ce qui posera moins de problème pour l'utilisation de la dépendance. Ce sera implémenté pour maven 4.x
* Maven Deamon sont un deamon qui va accélerer le build. Il a montré un exemple ou le premier build met 13 secondes et les suivants 0.0 secondes. Cela build de facon paralèle. Cela fonctionne déjà en maven 3.x

[Vidéo](https://www.youtube.com/watch?v=lT6FFbTfvXo)

### [Cloud public, mais données privées !](https://cfp.devoxx.fr/2022/talk/YKJ-2069/Cloud_public,_mais_donnees_privees_!)
C'est un outils pour cripter avant d'envoyer les données sur des clouds.

[]()

### [Save the date !](https://cfp.devoxx.fr/2022/talk/NMD-7139/Save_the_date_!)
Il faut stoquer la date avec le décalage de date dans les bases de données.

[Vidéo](https://www.youtube.com/watch?v=o6H6KksHDSA)

## Vendredi 22 avril 

[Programme](https://cfp.devoxx.fr/2022/byday/fri)

### [Kafka Streams @ Carrefour : du big data à la vitesse de l'éclair](https://cfp.devoxx.fr/2022/talk/JBP-9265/Kafka_Streams_@_Carrefour_:_du_big_data_a_la_vitesse_de_l'eclair)
Il faut penser à netoyer les topics interns et les consumer groups qui ne sont plus utilisées.

[Video](https://www.youtube.com/watch?v=4BU2UEDQQhs)

## [À la découverte des Docker Dev Environments](https://cfp.devoxx.fr/2022/talk/UQC-0994/A_la_decouverte_des_Docker_Dev_Environments)
C'est des contener sur le poste du dev. Permet de partager facilement le projet et l'environnement entre dev.

[Video](https://www.youtube.com/watch?v=MVyHEf-QxTI)

## [Tests Cucumber: légendes et réalité](https://cfp.devoxx.fr/2022/talk/TGD-8267/Tests_Cucumber:_legendes_et_realite)
Les tests cumcumber sont bien pour faire des tests fonctionnelles. Ils peuvent être fait en collaboration entre ceux qui spec et les dev. En general, ils sont lisibles par des non dev, et ça permet d'être sur de ce qui est testé correspond aux fonctions demandé par le client.

[Video](https://www.youtube.com/watch?v=-bnWa68JBcE)

## [Mieux maitriser TLS, OpenSSL et les certificats](https://cfp.devoxx.fr/2022/talk/NXR-6022/Mieux_maitriser_TLS,_OpenSSL_et_les_certificats)
Description du protocole TLS et des certificats.

[Video](https://www.youtube.com/watch?v=P6brMpIZaOo)

## Autre

Pour voir les nouveautés d'ElasticSearch entre les versions : https://github.com/blookot/elastic-releases

L'outils [Tournesole App](https://tournesol.app/) permet de juger la pertinance des sites web. C'est un travail collaboratif.
---
title: "Extra Leaderboard API"
date: 2023-04-02T12:00:00+05:30
draft: false
github_link: "https://github.com/Banalian/ExtraLeaderboardAPI"
author: Lilian Pouvreau
tags: 
    - "Java"
    - "JEE"
image: /projects/ELP/exemple2.jpg
description: API utilisée par le plugin Extra leaderboard pour Trackmania. Utilise Java Enterprise Edition. Utilisée par le plugin pour appeler l'API de Nadeo avec un compte qui n'a jamais joué, ce qui est requis pour obtenir certaines informations.
toc:
---

Cet API, réalisée en utilisant Java Enterprise Edition, permet de récupérer des données sur le jeu Trackmania, développé par Nadeo. Ces données sont ensuite utilisées par le plugin [Extra Leaderboard Position Plugin](/projects/ExtraLeaderboardPositionPlugin).

## Fonctionnalités

Cet API, qui respecte les standards REST, permet de récupérer les données suivantes :
- les positions du classement d'une course pour des temps donnés
- les temps de fin de course pour des positions données
- les temps de fin de course et positions hypothétiques pour des médailles données
- des informations sur les courses (temps des médailles, nombre de joueurs ayant un temps dans le classement, etc...)

Ces informations sont récupérées à partir de l'API de Nadeo, à l'aide d'un compte Ubisoft n'ayant jamais joué au jeu. Cela permet d'avoir accès à plusieurs informations qui sont normalement perdues lorsqu'un joueur joue aux courses, pour des raisons d'optimisation. Un exemple est que s'ils ont un certain meilleur temps sur une course, il n'est plus possible de recupérer la position d'un temps hypothétique supérieur pour cette course, ce qui empêche de récupérer les temps et positions hypothétiques pour les médailles.

## Fonctionnement interne

Afin d'avoir une application fonctionnelle, les principes suivants ont été mis en place :

- Un sous projet Web existe, et permet d'écouter les requêtes sur les différents endpoints de l'API. Cette partie effectue le moins de traitrements possible sur les données entrant et sortant de l'API, afin de respecter une séparation des responsabilités.
- Un sous projet Service/EJB existe, et permet de réaliser différents traitements sur les données. C'est cette partie qui contient toute la logique métier de l'API. Elle contient également tout le modèle de données, étant donné que c'est la seule partie de l'API qui s'en sert. (la partie web n'utilise qu'une classe étant la réponse à une requête)
- Un sous projet EAR, qui contient uniquement de la configuration afin de build et obtenir un exécutable fonctionnel.

Le fonctionnement interne général de l'API est le suivant :
- Une requête est envoyée à l'API, sur un endpoint donné.
    - L'API récupère les paramètres de la requête, et les transforme en objet Java. Il effectue potentiellement des vérifications et modifications sur ces paramètres.
- L'API appelle le service correspondant à l'endpoint et lui passe les paramètres.
    - Le service effectue potentiellement d'autres vérifications et modifications sur les paramètres, et fini de les transformer en objet Java.
    - Le service lance ensuite une chaine de responsabilités, qui va récupérer les données sur l'API de Nadeo et les traiter avant de les transformer en une réponse.
- Le service retourne la réponse au endpoint, qui la transforme en JSON, et la retourne à l'utilisateur.

En parallèle de cela, deux systèmes existent :
- Un système de filtre basique servant à tenir compte du temps de traitement de l'appel, et à donner un ID afin de suivre la requête.
- Un système servant à demander et rafraichir des tokens, nécéssaire aux appels à l'API de Nadeo.
    - Ce système est basé sur un timer, qui lance une tâche toutes les 55 minutes. Cette tâche va demander un nouveau token, et le stocker dans une classe statique. Lorsqu'une requête est envoyée à l'API, le token est récupéré, et utilisé pour l'appel à l'API de Nadeo. Si le token est expiré, une nouvelle requête est envoyée pour en obtenir un nouveau.

## Déploiement

Ce projet a également permis d'apprendre à se servir des Github Actions, afin de déployer automatiquement l'API sur un serveur distant, à chaque push sur la branche master (qui est en général dû à une pull request).

Cela permet qu'à chaque fois qu'une nouvelle version est pushée sur la branche master, les Actions vont essayer de build le projet, puis si cela réussit, il ira déploier l'API sur le serveur distant.

## AWS

L'API est déployée sur un serveur AWS EC2, ce qui permet de la rendre accessible à tous les utilisateurs du plugin, sans que cela soit relié à un ordinateur personnel. Cela m'a permis d'apprendre à utiliser AWS, et à déployer une application sur un serveur EC2, ainsi qu'à gérer un budget et des droits d'accès.


---
title: "Extra Leaderboard Position Plugin"
date: 2023-04-24T12:00:00+05:30
draft: false
github_link: "https://github.com/Banalian/ExtraLeaderboardPositions"
author: Lilian Pouvreau
tags: 
    - "AngelScript"
image: /projects/ELP/main.jpg
description: Un plugin pour Trackmania (utilisant Openplanet) pour afficher plus de positions dans le leaderboard. Utilise Angelscript, et optionnellement une API externe.
toc:
---

Ce plugin, réalisé pour Trackmania en utilisant OpenPlanet, permet d'afficher un nombre personnalisé de positions dans le classement, qui ne sont normalement pas facilement accessibles via l'interface de jeu.


Le plugin est disponible sur Openplanet : [Plugin](https://openplanet.dev/plugin/extraleaderboardpositions)

## Fonctionnalités

A l'aide de ce plugin, vous pouvez afficher plusieurs positions supplémentaire (comme par exemple la 10éme, 100éme, 1000éme, etc...) dans le classement. Il est également possible d'afficher les positions hypothétiques des médailles de la course.

(Images)

## Fonctionnement interne

Ce plugin a été réalisé en utilisant le framework [OpenPlanet](https://openplanet.dev/). Il utilise le langage de script Angelscript. Cela permet d'écrire des scripts qui sont ensuite compilés et interprétés par OpenPlanet dans le jeu Trackmania.

Le fonctionnement global est  le suivant :
- Toutes les X minutes (paramétrable), le plugin récupère les données du classement de la course en cours, selon les paramètres de l'utilisateur. (quelles positions, medailles, etc...)
    - Optionnellement, il est possible d'utiliser une API externe pour réaliser cette tâches, afin d'avoir accès à plus de données (voir la page de [Extra Leaderboard API](/projects/ExtraLeaderboardAPI)).
- Le plugin affiche ensuite ces données dans le jeu, à l'aide de l'API d'UI de OpenPlanet, qui utilise ImGui.
- En parallèle, le plugin écoute les évènements du jeu, afin de détecter quand une course est lancée, ou quand le joueur change de position dans le classement. Lorsqu'un de ces évènements est détecté, le plugin met à jour les données affichées.
- Enfin, le joueur peut à tout moment modifier ses préférences via les options du plugin.
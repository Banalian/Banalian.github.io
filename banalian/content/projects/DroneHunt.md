---
title: "Drone Hunt"
date: 2023-04-02T12:00:00+05:30
draft: false
#github_link: ""
author: Lilian Pouvreau
tags: 
    - "Unreal Engine 5"
    - "C++"
    - "Blueprint"
image: /projects/DroneHunt/main.jpg
description: Un TPS multijoueur en ligne, réalisé en 2 mois en utilisant Unreal Engine 5, dans le cadre d'un cours de programmation réseau dans le jeu vidéo.
toc:
---

Un TPS multijoueur en ligne, réalisé en 2 mois en utilisant Unreal Engine 5, dans le cadre d'un cours de programmation réseau dans le jeu vidéo.

## Contexte

Ce projet a été réalisé dans le cadre du cours de programmation réseau dans le jeu vidéo, en 2 mois, en équipe de 3 personnes. Le but de ce projet était de réaliser un jeu multijoueur en ligne, en utilisant Unreal Engine 5 et en utilisant EOS (Epic Online Services) pour la partie lobby/statistiques/etc.

## Gameplay

Le but du jeu est de détruire le plus grand nombre de drones ennemis, tout en étant en direct confrontation avec les autres joueurs pour atteindre ce plus grand score. Le joueur peut se déplacer, sauter et tirer. Il n'y a pas de tir entre les joueurs, et les drones ne sont pas hostiles, et au contraire essayent de fuir le joueur. 

Plusieurs types de drônes sont présents dans le jeu, avec un score différent pour chacun d'entre eux. Un type de drône permet même d'obtenir un bonus de vitesse si le joueur arrive à le détruire.

## Partie technique

Ce jeu est plutôt à considerer comme un prototype qui était une excuse pour prendre en main les concepts clé du développement réseau dans Unreal Engine 5. Dans ce projet, j'ai eu l'occasion de m'occuper de l'intégration d'EOS dans le jeu, ainsi différentes parties du gameplay et de la partie réseau du fonctionnement général du jeu.

### EOS

EOS (Epic Online Services) est un service en ligne proposé par Epic Games, qui permet de gérer la partie multijoueur en ligne d'un jeu. Il permet de gérer les parties, les statistiques, les amis, les succès, etc. Il est possible de l'utiliser avec Unreal Engine 5, et c'est ce que nous avons fait dans ce projet.

J'ai eu l'occasion de développer durant le cours (à l'aide du professeur) un plugin permettant d'utiliser ce Back-end. Ce plugin est ensuite utilisé dans le jeu pour gérer les lobby, les statistiques et les succès du jeu.

### Gameplay

J'ai eu l'occasion de m'occuper de la partie du développement du gameplay général du jeu (Gamemode, GameState, PlayerState, UI). J'ai également mis en place le système de lobby, à l'aide du plugin réalisé durant le cours. Mes collègues se sont occupés des mécaniques de gameplay et de l'IA des drones.

Tout ce travail m'a permis de mieux comprendre le fonctionnement général d'un jeu multijoueur en ligne, et de mieux comprendre comment Unreal Engine 5 gère la partie réseau, à l'aide de concept comme les RPC, les Delegate/Event, etc...

## Demo

Une vidéo de présentation sera prochainement disponible, afin de présenter les différentes fonctionnalités du jeu.
---
title: "Babillard3D"
date: 2023-01-02T12:00:00+05:30
draft: false
#github_link: ""
author: Lilian Pouvreau
tags: 
    - "Unity"
    - "C#"
image: /projects/Babillard3D/4.PNG
description: Application en VR sur le casque Meta Quest 2, permettant de créer des notes en 3D et de travailler en collaboration avec d'autres utilisateurs.
toc:
---

Une application en VR sur le casque Meta Quest 2, permettant de créer des notes en 3D et de travailler en collaboration avec d'autres utilisateurs. Réalisé dans le cadre du cours d'interaction 3D et Réalité virtuel en quelques semaines avec 2 autres étudiants.

## Description

Cette application avait pour but de permettre à des utilisateurs de se rejoindre dans un espace virtuel et de pouvoir y créer des notes en 3D. Ces notes consistaient en des textes, boîtes, liens et dessin pouvant être imbriqués les uns dans les autres. Les utilisateurs pouvaient également se déplacer dans l'espace et interagir avec les notes des autres utilisateurs.

Durant le développement, les features de dessin, boîte et liens ont été réalisé. J'ai pour ma part eu l'occasion de travailler à la création d'un système de sauvegarde d'espace de travail, et de m'occuper de l'intégration des autres systèmes et de la mise en place de l'architecture du projet VR.

## Aspect technique

Le projet a été réalisé en C# avec le moteur de jeu Unity en quelques semaines. Nous n'avons pas mis en place le système multi-utilisateur, mais nous avons tout de même mis en place le système de sauvegarde d'espace de travail, qui permet à l'utilisateur de garder son espace et de revenir plus tard pour le modifier.

### Système de sauvegarde

J'ai eu l'occasion de travailler sur le système de sauvegarde d'espace de travail, ce qui m'a demandé d'intégrer tous les autres systèmes existants. J'ai pour cela utilisé une librairie permettant d'effectuer des sérialisations de scènes/GameObjects sur Unity. Cette librairie fonctionnait bien pour nos besoins, mais vers la fin de projet, un souci au niveau du build à empêché d'avoir un fonctionnement parfait. Ce souci aurait pu être réglé avec plus de temps, en re-adaptant le système actuel pour sauvegarder un GameObject contenant l'espace de travail, plutôt qu'en sérialisant toute la scène sauf les éléments non nécessaires.


## Images

![Image 1](/projects/Babillard3D/1.PNG)
![Image 2](/projects/Babillard3D/2.PNG)
![Image 3](/projects/Babillard3D/3.PNG)
![Image 4](/projects/Babillard3D/4.PNG)
![Image 5](/projects/Babillard3D/5.PNG)
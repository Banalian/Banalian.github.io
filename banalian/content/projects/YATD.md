---
title: "Yet Another Tower Defense"
date: 2023-04-02T12:00:00+05:30
draft: false
#github_link: ""
author: Lilian Pouvreau
tags: 
    - "Unity"
    - "C#"
image: /projects/YATD/main.PNG
description: Un simple Tower Defense réalisé sur Unity. Attention aux ennemis, mais également à vos propres tours, qui peuvent se détruire entre elles. Réalisé en C#.
toc:
---

Un simple Tower Defense réalisé sur Unity. Attention aux ennemis, mais également à vos propres tours, qui peuvent se détruire entre elles.

## Contexte

Dans le cadre du cours de conception de jeux vidéo, j'ai eu l'occasion de réaliser ce Tower Defense en 3 mois dans une équpe de 3 personnes. Le but de ce projet était de réaliser un jeu de A à Z, afin de prendre en main les concepts clés de la conception de jeux vidéo, ainsi que le développement sur Unity.


## Concept

Yet Another Tower Defense est un Tower Defense se déroulant dans une époque médiévale fantastique. Notre héros, dernier protecteur du royaume du Fjord, va devoir mettre en place des mécanismes de défense afin de protéger le royaume des ennemis provenant d’un portail magique. Il va devoir procéder avec grande attention, car des rumeurs et légendes racontent que le portail fait ressortir les côtés les plus sombres de chaque habitant du Fjord.

La particularité du jeu est que le joueur et ses tours et mécanismes vont pouvoir se blesser entre eux, ce qui veut dire que le joueur devra placer stratégiquement ses tours afin qu'elles ne s’entre-détruisent pas. Il devra également faire attention à lui-même, étant donné qu’il pourra également être blessé par ses propres mécanismes de défense.

## Gameplay

Durant le jeu, le joueur devra survivre à plusieurs vagues d’ennemis afin de terminer le niveau actuel. Chaque vague comporte un certain nombre d’ennemis qui apparaissent d’un portail et suivront un chemin afin d'essayer d'atteindre le château du joueur. Le joueur devra donc placer des tours afin de détruire les ennemis avant qu’ils n’atteignent le château.

Plusieurs tours sont disponibles, chacune ayant des caractéristiques différentes : 

- La tour basique, ayant des statistiques équilibrées.
- La tour rapide, ayant une cadence de tir plus élevée, mais des dégâts plus faibles en contrepartie.
- Le mortier, ayant une cadence de tir très faible, mais des dégâts de zone assez conséquents, capable de détruire plusieurs ennemis à la fois.

En tuant des ennemis, le joueur gagne de l’or, qui lui permettra d’acheter de nouvelles tours, ou d’améliorer ses tours existantes.

La difficulté du jeu réside dans le fait que certains ennemis peuvent blesser les tours et que ces dernières peuvent également se détruire entre-elles, avec des projectiles mal placés. Le joueur devra donc faire attention à ne pas placer ses tours trop proches les unes des autres, afin d’éviter qu’elles ne se détruisent entre elles.

## Partie technique

Durant ce projet, j'ai eu l'occasion de travailler sur la plupart des systèmes, comme les tours, les ennemis, les projectiles, les vagues et le système général de jeu. J'ai également eu l'occasion de travailler en partie sur l'interface utilisateur.



## Images

![Image 1](/projects/YATD/enemy.jpg)

![Image 2](/projects/YATD/main.PNG)

![Image 3](/projects/YATD/lvl0.jpg)

![Image 4](/projects/YATD/lvl1.jpg)

![Image 5](/projects/YATD/lvl1_2.jpg)

![Image 6](/projects/YATD/map.jpg)

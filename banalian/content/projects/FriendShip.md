---
title: "Friend-Ship"
date: 2023-04-02T12:00:00+05:30
draft: false
#github_link: ""
author: Lilian Pouvreau
tags: 
    - "Unity"
    - "C#"
image: /projects/FriendShip/main.jpg
description: Un Shoot'em up avec un twist rempli d'amitié et de coopération.
toc:
---


Dans l’espace, un vaisseau spatial navigue grâce au pouvoir de l’amitié à travers des hordes d’adversaires. Son but: Tuer ou s’allier avec ces ennemis afin de survivre aux différentes vagues d'assaillants. 

## Contexte

Ce projet était au départ une démo réalisé sur Pico8 par un membre du groupe. Il a ensuite été réalisé dans le cadre d'un atelier en jeu vidéo (ainsi que sur le temps libre du créateur du projet ainsi que moi-même) afin de le porter sur Unity, et d'ajouter de nouvelles fonctionnalités et d'étendre le concept. Le groupe durant l'atelier était composé de 4 personnes.

## Concept

Friend-Ship est un shoot’em-up avec un style rétro demandant au joueur de combattre des vagues d’ennemis dans un niveau auto-scroller.

Ce shoot’em up à pour but de vous inciter à être agressif via son système de combo et de multiplicateur de score, sa particularité est une mécanique de conversion d’ennemis, permettant de plus facilement traverser les niveaux.

## Histoire
Dans l’univers pseudo-futuriste de Friend-Ship, les émotions sont la plus grande source de puissance de l’univers, elles ont des applications quasi-infinies, on les utilise notamment comme générateurs pour les vaisseaux spatiaux ou comme munitions pour les armes desdits vaisseaux.

Plusieurs factions utilisent des émotions négatives telles que la jalousie, la fierté ou la colère dans le but de contrôler l’univers, il incombe à notre protagoniste de les défaire avec le pouvoir de… L’amitié! Il est capable de débarrasser ses ennemis de leurs émotions négatives, les convertissant en puissants alliés pour combattre l’invasion des mauvaises émotions.



## Partie technique

Dans cette partie, je vais détailler plusieurs choix de conceptions qui ont été réalisés au cours de ce projet, en expliquant le raisonnement derrière ces choix et les résultats que ces choix engendrent. Ces choix concerneront surtout les parties du code sur lesquelles j’ai travaillé, à savoir le système de mouvement et de niveau.

### Choix généraux
Durant ce projet, nous avons décidé de prendre en main le système d'évent (via les Actions et UnityActions) d’unity, qui permet d’éviter des situations du style “faire une boucle qui attend que tel action se produise” et qui permet également d’éviter d’ajouter des dépendances fortes entre des classes. 
Ce système d'évent permet par exemple, lorsque le joueur se fait toucher, de déclencher automatiquement dès logique concernant le changement de point de vie, des potentiels FX, etc.., ce qui en conséquence déclenche d'autres modifications (la modification de la vie qui déclenche une modification de l’UI) par exemple.


### Système de Mouvement

Un système de mouvement extensible a été réalisé pour ce projet. Ce système à connu deux versions durant son développement.

#### Version 1

Cette version consistait en un script de mouvement de base, qui pouvait être étendu pour définir les mouvements à mettre en place (ligne droite, sinus, follow etc). Cela permettait d’éviter la répétition de code, et d’avoir une base commune à tous les mouvements. Ce système à cependant rapidement vu ses limites, lorsque j'ai voulu l’intégrer au système de tir, ou de spawn d'ennemis. Je souhaitais avoir un système assez flexible pour donner n’importe quel script de mouvement à un ennemi ou une balle, et modifier cela dans l’éditeur afin d’itérer plus facilement qu’en créant des dizaines de prefab contenant chacun des scripts de mouvement différent.

#### Version 2

Suite à cette première version, le système à été repensé afin de permettre cette flexibilité. Pour atteindre ce but, une séparation de la logique et des données à été effectuée Cette séparation permet d’avoir ces classes contenant uniquement des données nécessaire à un mouvement (une direction, une amplitude/fréquence pour un sinus, une cible, …). Suite à cela, les scripts de logique ont été modifiés afin d'utiliser ces données, et un script “MovementManager” a été créé afin d’instancier et modifier au besoin ces mouvements.

Suite à cela, différent script servant d’éditeur customisé ont été créé, afin de pouvoir modifier dans l’éditeur le fonctionnement de différent système, comme le fait de choisir pour l’édition de niveau le script de mouvement à donner à un ennemi par exemple (en n’ayant qu'à définir la donnée, qui sera ensuite donnée au MovementManager).

Au final, cela donne un système étendable facilement, et utilisable dans l’éditeur par d’autres systèmes, afin d’avoir autant de flexibilité que nécessaire pour rapidement itérer sur des versions de niveau différent par exemple.


### Système de Niveau

Afin d’avoir un niveau jouable, un système de niveau, de vague et de groupe d’ennemis a été mis en place. Afin de le comprendre, voyons les parties les plus petites, avant de revenir petit à petit au système global.

Comme dit précédemment, ce système utilise également les events de Unity afin de suivre la progression des systèmes.

#### Groupe d’ennemis

Dans ce jeu, un groupe d'ennemi représente un petit bataillon d'ennemi, représenté par l’ennemi à faire apparaître, sa position d’apparition, le mouvement que ce bataillon aura (qui sera donné individuellement à chaque ennemi du groupe), ainsi que d’autres données comme le temps à attendre entre chaque spawn etc.

#### Vague

Ici, une vague représente un groupe de groupes d'ennemis à faire apparaître. pour cela, on donne un groupe, et au bout de combien de temps il on doit le faire apparaître (soit un “timestamp”). Certaines données supplémentaires existent, comme le temps à attendre au départ. Actuellement, ces vagues sont des Scriptable Objects.

#### Niveau

Enfin, nous avons les niveaux. Un niveau est simplement une suite de vagues à faire apparaître, ainsi que des conditions pour passer à la vague suivante (un nombre d’ennemis à tué, un temps un attendre, ou alors commencer instantanément la vague suivante). En plus de ces conditions,quelques informations supplémentaires existent (temps entre deux vagues, durée d’une transition, etc…). Au final, cela permet d’avoir un système assez robuste, et modifiable entièrement dans l’éditeur, ce qui est encore une fois utilisé pour facilement itérer sur la création de niveaux.


## Situation actuelle

Lors de ce premier atelier, un protoype fonctionnel a été réalisé, permettant de tester les mécaniques de base du jeu, et de voir si le concept est intéressant. Le créateur du jeu et moi-même continuons actuellement le développement du jeu, afin de le rendre plus complet, et d'idéalement le sortir sur Steam au courant des prochains mois.


## Trailer

Voici le trailer du jeu, réalisé pour conclure ce premier atelier.

{{< youtube O5IPaBvK3d0 >}}
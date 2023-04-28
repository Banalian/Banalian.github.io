---
title: "Form Finder"
date: 2023-04-02T12:00:00+05:30
draft: false
#github_link: ""
author: Lilian Pouvreau
tags: 
    - "Unity"
    - "C#"
image: /projects/FormFinder/main.jpg
description: Un prototype de jeu sérieux sur le théme de l'IA.
toc:
---

Dans le cadre d'un cours de jeux sérieux, j'ai eu l'occasion de réaliser ce jeu avec l'aide d'une équipe de 6 personnes, en moins de deux mois. Le jeu a été réalisé avec Unity, en C#.

## Histoire

(Extrait de l'introduction du jeu)

Bienvenue dans l'équipe de <TakeShape>, <NewEmployee.getName>.

Je suis là pour vous aider à naviguer dans notre environnement de travail.

La société s'est donnée pour mission de battre notre concurrent <Geo-ShAIpe> à son propre jeu.

Nous savons que notre rival utilise une IA de tri ultra-performante pour sa chaîne de production.

Vous allez devoir résoudre des puzzles en triant correctement des objets d'entrée dans différentes sorties.

Pour cela vous utiliserez des machines dotées de traitements uniques et améliorerez votre chaîne de production.

Nous sommes impatients de voir tout ce que vous pouvez apporter à notre entreprise <NewEmployee.getName>.

## Gameplay

Ce jeu comporte deux coeurs de gameplay distincts :
- Un gameplay en 3D, où le joueur sera en mesure de se déplacer dans l'usine et d'interagir avec une console pour lancer les niveaux.
- Un gameplay en 2D, où le joueur devra résoudre des puzzles de tri, en utilisant différentes machines, comme des filtres ou des séparateurs. Lors de ces puzzles, le joueur 
sera amené à utiliser des machines de plus en plus complexes, et à les combiner entre elles afin de résoudre des puzzles de plus en plus complexes également.

## Aspect du Jeu Sérieux

Le but de ce jeu sérieux était de démystifier l'IA, en poussant à l'extrême l'idée que certaines IA sont en réalité "Juste des 'if' qui se suivent". Le jeu est donc basé sur le tri d'objets, et le joueur doit utiliser des machines pour trier ces objets. Le joueur aurait ensuite l'occasion de se rendre compte qu'au fur et à mesure des puzzles, il réussi à réaliser des tâches de plus en plus complexes, en utilisant des machines représentant par exemple d'anciennes solutions, ce qui reviens à simplement avoir découpé le problème en plusieurs sous-problèmes plus simples.

## Partie Technique

Sur ce projet, j'ai eu l'occasion de travailler sur plusieurs aspects techniques de la partie 2D du jeu comme la représentation des données des formes, l'intégration des systèmes, le système de machines, et le système de niveau. 

### Le système de machines

 ![Gif des machines](/projects/FormFinder/AllMachines.gif)


Ce système fonctionne en essayant un maximum de réduire la duplication de code, et de faciliter un maximum la création de machines en tant que game designer. Pour atteindre ce but, la logique des machines ont été séparées en deux parties :
- La récupération des formes d'entrée, qui se déroule via l'ajout de "grabbers" qui déclanchent des évènements lorsque des formes sont récupérées.
- La machine elle-même, qui contient la logique de traitement et de sorties des formes traitées.

Cette seconde partie a été réalisée en limitant un maximum la duplication de code comme énoncé précédemment. Pour cela, j'ai créé une interface et une classe abstraite contenant toute la logique globale d'une machine, comme la récupération de formes dans une liste d'attente, le déclanchement de coroutines, ou la logique globable d'éxécution d'un traitement. Les classes filles de cette classe abstraite n'ont donc plus qu'à implémenter la logique de traitement de la machine, et à définir les paramètres spécifiques à cette dernière.

Notre jeu contient uniquement un séparateur, des filtres et un incinérateur, mais essayons d'imaginer une machine qui change la couleur d'un objet, voici le pseudo-code de la classe de cette machine :

```csharp
public class ColorChanger : AMachineBase
{

    /// <summary>
    /// La couleur à appliquer aux formes
    /// </summary>
    Color color;

    /// <summary>
    /// Détermine si on peut lancer le processus de traitement
    /// </summary>
    public override bool CanLaunchProcess()
    {
        return WaitingParts.Count >= 1 && !IsProcessing;
    }

    /// <summary>
    /// Logique de préparation du traitement
    /// </summary>
    protected override void BeforeProcess()
    {
        base.BeforeProcess();
        Parts.Add(WaitingParts[0]);
        WaitingParts.RemoveAt(0);
    }

    /// <summary>
    /// Logique de traitement
    /// </summary>
    protected override IEnumerator Process()
    {
        // Changement de couleur de la forme
        var part = Parts[0];
        part.color = color;
        //  On vide la liste des formes du traitement
        Parts.Clear();
        yield break; // ou WaitForSeconds si on veut un délai de traitement

        // on fait ressortir la forme de la machine, en recréant une forme à partir de la donnée traitée
        // Cette fonction serait définie par cette classe, car il faudrait spécifier le point de sortie, à l'aide des données déjà présentes dans la classe.
        SpawnPart(part);
    }
}
```

Et cela suffit, tout le reste est géré par la classe abstraite et le game designer n'a plus qu'à se concentrer sur la logique de traitement de la machine.

### Le système de niveau

Quand on parle de système de niveau ici, on parle de système gérant la logique d'un niveau, comme les formes qui vont être utilisées, les machines disponibles, les conditions de victoire, ainsi que plus généralement la logique d'état de jeu (Edition, Jeu, etc...).

#### Édition / Jeu
 
 Afin de pouvoir progresser dans le jeu, on observe deux parties distinctes dans la résolution d'un niveau :
 - L'édition du niveau, où le joueur peut placer des machines, les configurer, et les relier entre elles via des convoyeurs.
 - Le jeu, où le joueur peut lancer le niveau, et voir si sa solution fonctionne, sans pouvoir modifier sa solution pendant l'éxécution du niveau.

 Pour cela, les UnityAction de Unity ont été utilisées. Les UnityActions sont des sortes d'event, auquel des classes peuvent s'abonner, afin d'invoquer des fonctions lorsqu'un évènement se produit. Ici, cela permet d'avoir un event de déclanché quand le joueur décide d'appuyer sur le bouton d'édition, ou sur le bouton de jeu. Les classes qui ont besoin de savoir si le jeu est en mode édition ou en mode jeu peuvent donc s'abonner à cet event, et changer leur comportement en fonction de l'état du jeu (par exemple, on supprime toutes les formes du jeu quand on passe en mode édition et on réinitialise les machines).

#### Données d'un niveau

J'ai eu l'occasion de créer des ScriptableObjects permettant de représenter les niveaux. pour cela, on a différentes informations, comme le nombre d'entrées avec le contenu de chaque entrée, le nombre de sorties avec le contenu de chaque sortie requise pour terminer le niveau, ainsi que les machines disponibles. Cette partie a été réalisée en tandem avec l'équipe qui s'occupait du fonctionnement de la grille et du placement des machines.


## Démo


{{< youtube hTqForS1lpo >}}



## Conclusion

Je suis conscient que ce prototype manque de polish et que le message n'est pas forcément assez clair sur le point du jeu sérieux. Cependant, je suis tout de même content du résultat, car j'ai eu l'occasion de travailler sur des aspects techniques intéressants et je suis content des systèmes que j'ai pu mettre en place. Ces derniers permettent de facilement créer du contenu pour le jeu, ce qui était un des objectifs que je m'étais fixé au début du projet.

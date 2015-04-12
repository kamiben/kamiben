---
layout: post
title: "Ruby: Variables multilignes"
comments: true
category: Ruby
tags: []
---

Pour créer un retour chariot dans une chaine de caractères, il est possible d'utiliser le caractère d'échappement \n.

Cependant cette approche n'est pas forcément lisible si la variable présente plusieurs lignes. Il est possible de créer une variable multiligne de la manière suivante : 

    variable=<<TEXT
    Voici le contenu de la variable
    Présenté sur plusieurs lignes
    Il n'est pas nécéssaire d'utiliser le caractère d'échappement.
    TEXT
    
A noter qu'il est important de ne pas mettre d'espaces entre le symbole égal et <<.
---
layout: post
title: "Ruby : les operateurs unaire"
comments: true
category: Ruby
tags: []
---
J'ai découvert aujourd'hui les opérateurs unaire en ruby (unary operators).

L'occasion de se rendre compte qu'on les utilise régulièrement mais que leur nom nous est inconnu.

En math, une opération unaire est une opération avec un seul membre. En ruby, c'est similaire, un opérateur unaire ne prend qu'un seul argument. Par exemple le - de -8 ou ! de !true.

Il est opposé à l'opérateur binaire, qui prend deux arguements, comme 2 + 3. 

Ainsi, par défaut, l'opérateur unaire - permet de définir un nombre négatif, tandis que + définit un nombre positif. Il existe également le ~ qui renvoie l'opposé binaire d'un entier. Enfin, ! renvoie l'opposé d'un opérateur true or false.

L'article qui m'a permis de découvrir le concept est l'article très complet de [rubyinside](http://www.rubyinside.com/rubys-unary-operators-and-how-to-redefine-their-functionality-5610.html) sur ce sujet, mais qui traite de la redéfinition de ces opérateurs.
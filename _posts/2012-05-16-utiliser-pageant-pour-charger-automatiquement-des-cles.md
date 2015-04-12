---
layout: post
title: "Utiliser Pageant pour charger automatiquement des cles"
comments: true
category: Divers
tags: []
---

Pageant est un outil intégré à Putty permettant de garder des clés en mémoire. L'outil se trouve dans le dossier d'installation de Putty. Cependant il est pénible de les charger à la main. 

Heureusement Pageant permet de charger automatiquement une ou plusieurs clés privées au lancement.
Il suffit de les passer en paramètre sur la ligne de lancement (ou sur le raccourci) :

     C:\PuTTY\pageant.exe d:\main.ppk d:\secondary.ppk

(Pour le raccourci ajouter un espace après le dernier guillemet et entrer les chemins vers les clés sans guillemet)
Si les clés sont protégées par mot de passe, il vous sera demandé au lancement, impossible d'y couper.
Si Pageant est déjà lancé, les clés seront ajoutées au process existant.  

Pratique ! 
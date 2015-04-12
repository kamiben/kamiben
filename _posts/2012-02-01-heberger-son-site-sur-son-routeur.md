---
layout: post
title: "Héberger son site sur son routeur"
comments: true
category: Hebergement
tags: []
---

Ce site est hébergé sur mon routeur Asus WL 500Gp, flashé avec un firmware [openwrt](https://openwrt.org/) et utilisant ma connexion personnelle.

Le serveur qui vous sert ces pages est [lighttpd](http://www.lighttpd.net/). Il est configuré pour servir deux sites : jeu.arthion.fr et tech.arthion.fr.

Ceci est réalisé en ajoutant quelques lignes au fichier lighttpd.conf [un guide complet](http://www.cyberciti.biz/tips/howto-lighttpd-web-server-setting-up-virtual-hosting.html)


    ## jeu.arthion.fr
    $HTTP["host"] =~ "jeu.arthion.fr" {
    server.document-root = "/www/games/_site"
    }



J'utilise le moteur de blog (un parseur de texte en ruby) [Jekyll](https://github.com/mojombo/jekyll) afin de générer les pages du sites en format HTML à partir de fichier texte rédigés avec la syntaxe Markdown. 

Lors de la création du site, j'ai utilisé comme base les deux ressources ci-dessous très utiles pour découvrir jekyll : [Jekyll bootstrap](http://jekyllbootstrap.com) et ... [Jekyll bootstrap template](https://github.com/jgritman/Jekyll-Bootstrap-Template)

Pour la feuille de style, j'utilise le boilerplate [Bootstrap](http://twitter.github.com/bootstrap/) de Twitter. 

Enfin, pour la partie esthétique, j'ai adapté du mieux que j'ai pu l'excellent thème wordpress [Vostok](http://www.vostoktheme.com/)

Les sites sont mis à jour à l'aide de git. Le theme est disponible sur https://github.com/kamiben/Jekyll-bootstrap2-template--french-

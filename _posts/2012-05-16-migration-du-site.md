---
layout: post
title: "Déploiement du site"
comments: true
category: Jekyll
tags: []
---

J'ai migré le site sur un VPS, après plusieurs mois sur le routeur. Ce fonctionnement a été une réussite et a correctement fonctionné sans aucun accroc sur toute la durée.

Le gros inconvénient motivant la migration est que je ne pouvais pas générer le site directement sur le routeur, par faute de ressources trop faible. Il était donc nécéssaire de générer le site en local, soit dans une VM Ubuntu, ce qui n'est pas particulièrement aisé pour poster au quotidien. (Lancer une VM uniquement pour écrire un post est un peu rebutant.)

J'ai donc opté pour un petit VPS pour :  
- Parfaire ma maitrise de l'administration Linux (le VPS tourne sous une débian)  
- Pouvoir générer le site directement sur la machine

Cela me permet donc de simplement éditer mes articles sur toutes mes machines, et de les envoyer via git sur le serveur.

Une fois arrivé sur le serveur, j'ai créé un Post-receive hook afin d'éxecuter automatiquement les commandes suivantes, basé sur les [conseils suivants](https://github.com/mojombo/jekyll/wiki/Deployment):

    GIT_REPO=$HOME/myrepo.git
    TMP_GIT_CLONE=$HOME/tmp/myrepo
    PUBLIC_WWW=/var/www/myrepo

    rvm gemset use jekyll
    git clone $GIT_REPO $TMP_GIT_CLONE
    jekyll --no-auto $TMP_GIT_CLONE $PUBLIC_WWW
    rm -Rf $TMP_GIT_CLONE
    exit

Ce qui permet à chaque git push de générer le site directement en production. Ce premier article sera le premier test pour ce mode de déploiement ;)

Normalement ce nouveau fonctionnement me simplifiera grandement l'envoi d'article, et donc me permettra de poster plus souvent ! J'espère pouvoir poster des articles sur l'administration de VPS, ruby et autre.

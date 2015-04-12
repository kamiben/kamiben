---
layout: post
title: "Héberger son serveur git privé"
comments: true
category: Hebergement
tags: []
---

Prérequis au déploiement de ce site, (enfin, il existait d'autres solutions, mais j'ai choisi git pour la gestion du blog), il a été nécéssaire de mettre en place un serveur Git sur le VPS.

Cela est également l'occasion d'y heberger les dépots privés (ce blog, jeu.arthion.fr, quelques petits projets qui ne sont pas dignes d'être sur [github](http://github.com/)), et pour un aussi petit volume de dépots, il n'était pas nécéssaire de prendre un abonnement payant.

Voici donc en quelques étapes comment mettre en place un serveur git sur son serveur. Ca va être rapide ;).

Mise en place du serveur
-----------------------
Ces instructions sont pour un VPS tournant sous Débian 5, mais devraient rester identiques sur Ubuntu.

Pour isoler les dépots du reste du système, et permettre un éventuel partage de dépot avec des amis,  on va créer un utilisateur appelé git :
  
    sudo adduser git 
  
A partir de là, on va ajouter les clés pour permettre une authentification sans mot de passe : 

    sudo mkdir /home/git/.ssh
    sudo chown -R git:git /home/git/.ssh
    sudo chmod 700 !$
  
Sur la machine de developpement :  
  scp ~/.ssh/id_rsa.pub git@server.com:.ssh/authorized_keys

On sécurise la clé sur le serveur :
    sudo chmod 600 /home/git/.ssh/*
  
Il est désormais possible de vous authentifier sans mot de passe en tant qu'user git, on va tester sur la machine de dev: 
    ssh git@server.com 
  
Ajouter les dépots sur le serveur
------------------
Sur le serveur, effectuez cette commande pour initier un dépot vide, a répéter pour chaque dépot qu'on voudra transférer depuis la machine de dev :
    git --bare init nom_dépot.git
  
Quittez le serveur, les dernieres étapes sont à effectuer en local.

Configurer la machine de développement 
-------------------------------------
Si vous avez déjà configuré votre dépot pour Github par exemple, on va supprimer le remote déjà enregistré avec : 
    git remote rm origin
  
A noter qu'il est également possible de nommer le remote vers votre serveur autrement, cette étape est donc optionnelle.

On ajoute alors le nouveau remote : 

    git remote add origin ssh://git@myserver.com:2207/~/myrepo.git
    git push origin master
  
Et voila ! Si vous souhaitez conserver le remote origin déjà en place, utilisez un autre nom (j'utilise vps). Mes commandes push sont alors git push vps master.

Pour ne pas avoir à répéter origin master, on peut indiquer à git le remote et une branch par défaut :
    git config branch.master.remote origin && git config branch.master.merge refs/heads/master
  
Et voila, désormais vous pouvez utiliser git push et git pull et vos dépots seront sauvegardés sur votre serveur.

Nota : Si vous souhaitez un environnement multi-utilisateur avec un fort controle sur les dépots, je vous invite à vous renseigner sur [Gitolite](http://wiki.github.com/sitaramc/gitolite/)
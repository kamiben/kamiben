---
layout: post
title: "Debrief sur une attaque web"
comments: true
category: Hebergement
tags: []
---

Par un frais soir d'hivers, au détour de quelques pages web, je fais un tour sans forcément de raison sur un de mes blogs wordpress.

Quelle horreur quand j'ai découvert que le site n'était plus accessible. Apparemment, php5 n'était plus activé. Ceci étant défini par un fichier.htaccess chez OVH, je me connecte sur mon hébergement par FTP.

Je récupère le .htaccess fautif et constate qu'il a été altéré pour comprendre des redirections en fonction d'user agent. Mais surtout qu'ils se sont plantés et qu'ils ont cassé le blog.

Immédiatement inquiet, je cherche à trouver quels sont les fichiers modifiés et surtout depuis quand.

####Trouver tous les fichiers mis à jour depuis X jours (X = nombre de jours)

{% highlight ruby %}    find . -mtime -X
{% endhighlight  %}
A l'aide de cette commande je trouve que tous les fichiers .htaccess de mes sites ont été modifiés le même jour, la veille. 

Afin de déterminer la source de la faille, je consulte les logs chez OVH (quelques recherches google m'ayant montré que le probleme pouvait venir d'un compte FTP compromis, je cherche à voir les logs FTP.

L'adresse pour consulter ces logs est la suivante : https://logs.ovh.net/adresse_hebergement/

Cela me permet de constater qu'en effet, la faille vient de là. Je bloque immédiatement l'accès par FTP, et commence à remettre en place les fichiers d'origine via SCP, en utilisant les snapshots d'OVH accessible à l'adresse FTP habituelle mais en modifiant le login par login-snapX, avec X = 1 3 5 30 en fonction du nombre de jours souhaités.

Les sites étant de nouveau d'aplomb et fonctionnels, je ne peux m'empecher de me demander si le compte est compromis depuis longtemps. 

L'épluchage des logs remonte une trace depuis l'été précédent, avec quelques fichiers ajoutés à mon insu, mais sans toujours aucun téléchargement de fichier compromettants.

Néanmoins, je modifie tous les mots de passe d'accès aux bases de données, et je réinstalle à neuf toutes les parties de mes sites.

####Lecon retenue : 

FTP est un protocole véritablement dépassé, qui transmet les mots de passe en clair. Une de mes connexion à du etre interceptée, ou le mot de passe FTP a tout simplement été brute forcé.


Désormais l'accès FTP est désactivé pour mon hébergement, sauf en cas de besoin.

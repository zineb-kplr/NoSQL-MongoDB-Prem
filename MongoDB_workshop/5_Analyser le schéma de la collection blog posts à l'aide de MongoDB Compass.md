# 5.Analyser le schéma de la collection blog posts à l'aide de MongoDB Compass.

Dans cette tâche, nous allons utiliser MongoDB Compass pour analyser le contenu de notre collection.

* Ouvrir MongoDB Compass:

![image](https://user-images.githubusercontent.com/73080397/212380556-6bacbff1-a6e1-478c-869b-1e731562aeb6.png)

* Puisque MongoDB est maintenant exécuté sur notre hôte local en utilisant le port par défaut, qui est 27017, nous n'avons pas besoin d'une chaîne de connexion et nous pouvons simplement cliquer sur le bouton **connect**. 

![image](https://user-images.githubusercontent.com/73080397/212380639-80a36d0c-cfaf-45a8-bd5d-1e7192efca6a.png)

* Nous pouvons voir notre instance MongoDB, et la liste des bases de données qu'elle contient. Nous pouvons trouver notre vieil ami admin, que nous avons exploré dans la première tâche, et ensuite la base de données bloh, que nous avons créée dans les trois tâches précédentes. Nous pouvons voir sa taille, le nombre de collections qu'elle contient et le nombre d'index, que nous explorerons plus tard. Il y a également un bouton "Trash" qui nous permet d'abandonner la base de données si nous le souhaitons

![image](https://user-images.githubusercontent.com/73080397/212381436-2d2bf9a0-0d28-4fd2-a63f-3883c39e323a.png)

* Cliquez maintenant sur la base de données de notre blog. Là encore, nous pouvons voir un résumé de la base de données, la liste des collections qu'elle contient. Dans notre cas, il n'y a qu'une seule collection, celle des posts.

![image](https://user-images.githubusercontent.com/73080397/212381914-736b3ac5-ec46-4caa-93e3-2c45d5acb267.png)

* Nous pouvons voir qu'elle contient 4 documents. Nous pouvons voir la taille moyenne des documents stockés dans cette collection, la taille totale des documents, le nombre et la taille des index dans la collection. Encore une fois, nous verrons plus tard l'utilité des index. 

* Cliquons sur la collection **posts**. Comme vous pouvez le voir, nous pouvons consulter les documents que nous avons stockés dans notre collection plus tôt. Nous pouvons, par exemple, développer le tableau des balises ou les objets auteur ou emplacement. Nous pouvons également voir nos documents à l'aide d'une vue en liste, ce qui est le cas par défaut, nous pouvons les voir dans une vue JSON ou dans une vue en tableau :

![image](https://user-images.githubusercontent.com/73080397/212382344-323664fc-437b-407b-a929-bd190a89b953.png)

Nous pouvons également modifier un document. Dans la vue d'édition, nous pouvons développer ou réduire à nouveau le tableau des balises et les documents intégrés pour montrer ce qu'ils contiennent. Nous pouvons également supprimer et ajouter de nouveaux champs, et nous pouvons voir le type de chaque champ ici, et nous pouvons le changer en n'importe quoi d'autre si nous le voulons. 

* Maintenant, appuyons sur Annuler. Jetons un coup d'oeil à la section schéma. Rappelez-vous que nous avons dit que MongoDB est sans schéma. Avec cette section, nous pouvons jeter un coup d'oeil à la structure de ce qui se trouve dans la base de données. Comme vous pouvez le voir dans la description, elle nous permet de visualiser rapidement notre schéma pour comprendre la fréquence, les types et les plages de champs dans notre ensemble de données. 

* Cliquez sur le bouton Analyser le schéma. 

![image](https://user-images.githubusercontent.com/73080397/212384983-d40e40e4-a132-45a3-966d-8c0b27599381.png)

* Nous pouvons voir que :
  * Nous avons 4 documents, et que le rapport est basé sur les 4 documents;
  * Nous avons la liste de tous les champs qui sont dans notre base de données, triés par ordre alphabétique;
  * Qu'il y a des documents qui ont le champ `_id`;
  * 100% de nos documents ont un champ `_id`, qui est un `objectID`, le type par défaut pour les ID MongoDB. 
  * Sur le côté droit, nous avons un graphique qui nous montre le jour de la semaine et les heures pendant lesquelles les documents ont été créés. 
  * Nous avons également la date et l'heure de la première et de la dernière création. Ceci est dû au fait que le hash de l'objectID contient ces informations. 
  * Ensuite, nous avons le champ author. 
  * Si vous vous souvenez, les auteurs étaient des documents intégrés, mais tous nos documents n'avaient pas le champ auhor. 
  * 50% de nos documents ont un champ auteur, qui est lui-même un document, tandis que le reste est indéfini. 
  * Si nous cliquons sur le triangle,  nous pouvons développer le contenu et nous pouvons voir que tous les documents qui ont un champ author;
  * 100% d'entre eux ont un champ de nom et de prénom, et nous pouvons voir qu'ils ont tous un contenu de chaîne; 
  * 100 % des documents ont un champ body, et qu'ils contiennent tous une chaîne de caractères. 
  * Tous les documents contiennent une date, et nous pouvons voir un rapport des dates, selon l'objectID. 
  * 75% de nos documents contiennent un double, et 25% n'ont pas du tout le champ, il est indéfini. 
  * 75% de nos documents ont des coordonnées, et nous pouvons également voir une carte qui nous montre l'emplacement réel stocké dans nos documents : San Francisco, Austin, et ici New York. 
  * Ensuite, nous avons le champ published. Tous ces champs sont booléens, et tous sont faux. 
  * Ensuite, nous avons le champ tags : 25% de nos documents contiennent un tableau, dont tous, 100% d'entre eux contiennent des chaînes de caractères. Enfin, le titre. 
  * Enfin, nous nos documents ont le champs title, et tous sont des chaînes de caractères. Et, comme vous pouvez le voir ici, 50% d'entre eux ont la chaîne "Awesome Post" stockée dans le champ.

Une autre raison pour laquelle nous examinons la section du schéma est que, en l'utilisant, nous pouvons plus facilement apprendre et voir quelques autres façons d'interroger nos documents. 

* Cliquer sur la chaîne **Awsome Post**

![aws_post](https://user-images.githubusercontent.com/73080397/212388211-5761df07-c8db-48ab-811d-4559a063238d.png)

* Regardons le texte du filtre. Comme vous pouvez le voir, nous avons une requête que nous avons déjà apprise auparavant, en spécifiant simplement le nom du champ et le contenu que nous recherchons. C'est ce que nous utiliserions dans une méthode `find()`, ou comme premier paramètre de la méthode `update()`
* Maintenant, appuyez sur la touche Shift et cliquez sur "MongoDB rules". Vous voyez que le texte du filtre a changé. Nous recherchons maintenant tous les articles qui portent le titre "Awesome Post" ou "MongoDB rules". Pour ce faire, MongoDB Compass a utilisé l'opérateur `$in`, qui attend un tableau, dans ce cas des chaînes de caractères. 

![aws_post](https://user-images.githubusercontent.com/73080397/212390444-5757dd1f-e4f6-4679-8d2c-d76915e8671d.png)

* Désellectionner les deux chaînes de caractères, aller sur le champ author et sélectionner un prénom:
* Sélectionner un prénom et remarquer que la notation par points est apparue dans le filtre:

![aws_post](https://user-images.githubusercontent.com/73080397/212391567-54fee95d-c793-44fe-8d06-f83031eab517.png)

* Désellectionner le prénom et aller dans le champs **location**

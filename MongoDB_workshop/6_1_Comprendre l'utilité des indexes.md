# 6.1.Comprendre l'utilité des indexes

Dans cette tâche, nous allons comprendre l'utilité des index. 

* Quitter le Shell Mongo :
```
exit
```

* se rendre dans le mgodatagen pour générer la data aléatoire  pour MongoDB:

```
cd mgodatagen
```
télécharger le fichier dataset.json et le déposer dans le même dossier que l'exécutable mgodatagen

Créer 5 000 000 documents à partir de datset.json :
```
./mgodatagen -f dataset.json
```

![image](https://user-images.githubusercontent.com/73080397/212576336-4d6f61b4-797c-4c3a-8d97-a277dcfe78f0.png)

Vous pouez remarquer la création de la collection **posts_big** avec 5 millions de documents à l'intérieur, vous vouvez également consulter la taille du fichier.

<img width="957" alt="cap_lin" src="https://user-images.githubusercontent.com/73080397/212577227-e5fadf3e-1beb-4a8b-9120-26048f2eb42e.png">

* Aller dans la collection **posts** > Schemas > Analyze Schema > title > cliquer sur **Awsome Post** > Cliquer sur Analyse à côté du filtre.

![image](https://user-images.githubusercontent.com/73080397/212578090-07fcc677-2a62-4b72-8634-75b2a1399e84.png)


 Nous pouvons voir que la requête a été exécutée et que deux documents ont été renvoyés. Mais comment cela se fait-il ? Bien sûr, la recherche d'un document dans une base de données prend un certain temps, et la base de données doit rechercher le document que nous voulons d'une manière ou d'une autre.
 
 * Aller dans **Explain Plan** et cliquer sur **Execute Explain** 

![image](https://user-images.githubusercontent.com/73080397/212578566-af4f27d2-0c20-4731-b24a-ab5165d67b18.png)


 nous pouvons voir le résumé des performances de la requête. C'est quelque chose que nous voulons toujours vérifier et faire lorsque nous créons et gérons une base de données. Nous voulons qu'elle soit performante, et cela dépend de ce que l'application recherche dans les données, et de la façon dont la base de données est organisée pour s'adapter à ces requêtes.
 
* Nous pouvons voir que nous avons deux documents retournés, comme prévu. 
* La requête totale a pris 0 milliseconde pour s'exécuter, donc probablement un temps très, très bref. 
* Ensuite, nous avons 0 clé d'index examinée, ce que nous expliquerons plus tard. Pour l'instant, notez simplement que le nombre est de 0. 
* Plus important encore, nous voyons que la base de données a dû examiner 4 documents, donc tous, pour trouver notre article par titre. 

![image](https://user-images.githubusercontent.com/73080397/212862698-63c2c1c4-1584-47c1-ab6f-1983367e7dac.png)


 Ceci est confirmé par la partie inférieure, qui est la liste des étapes que la base de données a suivies pour trouver notre document. Nous voyons que, encore une fois, en 0 milliseconde, donc un temps très court, elle a examiné 4 documents pendant un COLLSCAN (un scan de collection). Cela signifie qu'il a dû vérifier tous les documents un par un, afin de trouver les articles avec le titre que nous avons demandé.

Cela ne semble pas très efficace, n'est-ce pas ? Vous pourriez demander, quel est le problème ? Il l'a fait en 0 milliseconde. C'est super rapide de toute façon. Mais... pas si rapide. 

* Retournons à notre collection **post_big**. 
* Maintenant, allons au schéma, et analysons-le à nouveau: avant de le faire, cliquons sur les options, et mettons le temps maximum en millisecondes **MaxTimeMS** à 120 000. Il s'agit d'une base de données assez importante, après tout, et nous ne voulons pas que l'exécution soit arrêtée prématurément après 5 secondes, si elle prend plus de temps:

* Aller au champ "Title" et cliquer sur le premier titre qui apparaît :

![image](https://user-images.githubusercontent.com/73080397/213491782-7a50c5f2-381f-4972-936f-95b9308f27e0.png)

* Aller sur Explain Plan > Explain et identifier la durée en millisecondes de l'exécution (Actual Query Execution Time) et de l'opération pour trouver le document (Coollscan) :

![image](https://user-images.githubusercontent.com/73080397/213502079-0688e7dd-4270-45ce-a902-8d6aab671c60.png)

Remarquez comment MongoDB a dû examiner les 5 millions de documents pour trouver celui que nous voulions. Vous avez l'impression que l'accès aux documents va être de plus en plus lent au fur et à mesure que la base de données s'agrandit... et c'est exactement ça. Et c'est là que les index entrent en jeu. Un index est comme l'index d'un livre, et il est est automatiquement maintenu par la base de données, afin de trouver des documents simplement en regardant l'index lui-même, sans avoir à vérifier chaque document.   

* Essayons-le en allant dans la section des index:

![image](https://user-images.githubusercontent.com/73080397/213508280-88eb642b-0fbb-4a86-bb44-e3e460a57172.png)

Nous voyons qu'il y a déjà un index, qui est celui qui est toujours créé automatiquement par MongoDB sur le champ _id. 

Create Index > nom: "title" > sélectionner le champ title > lui donner un ordre ascendant > Create Index:

![image](https://user-images.githubusercontent.com/73080397/213511039-2e9b98c6-5fbb-4e53-8d2d-e823d08977e8.png)

Nous avons quelque chose qui augmente la vitesse, mais nous avons un coût en espace de stockage.

* revoyons notre section Explain Plan. Prenez note de ce temps d'exécution énorme, et cliquez sur Explain. 

![image](https://user-images.githubusercontent.com/73080397/213512529-3149a00f-b831-4df4-8534-065d07fcdd37.png)

Voyez ce qui se passe! N'est-ce pas incroyable ? Le temps d'exécution est maintenant de 1 milliseconde : c'est presque instantané. La base de données n'a pas eu à examiner 5 millions de documents. Elle a examiné la clé d'indexation, et elle n'a eu à examiner qu'un seul document.

Dans la partie inférieure de votre écran, nous pouvons voir que nous n'avons plus un balayage de collection, mais un balayage d'index, en utilisant l'index avec le nom "title", puis le document a été récupéré. Les deux choses se sont produites instantanément.

Félicitations ! Vous avez maintenant compris l'importance vitale des index dans une base de données. Vous avez appris les bases de l'examen d'une requête et de la création d'un index pour l'optimiser. 

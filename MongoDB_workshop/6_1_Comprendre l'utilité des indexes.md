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

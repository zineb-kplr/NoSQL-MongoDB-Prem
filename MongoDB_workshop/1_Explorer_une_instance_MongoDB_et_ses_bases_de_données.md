# 1.Explorer une instance MongoDB et ses bases de données

Dans ce workshop, vous allez créer une base de données MongoDB et l'optimiser en utilisant des index, à la fois au moyen du shell Mongo Shell et de l'interface graphique MongoDB Compass, tout en apprenant les bases des bases de données documents NoSQL.
NoSQL signifie "Not Only SQL", SQL étant le langage commun utilisé pour piloter les bases de données relationnelles traditionnelles. 

Il n'existe pas de solution unique qui soit parfaite pour tous les contextes. L'utilisation de bases de données NoSQL présente donc des avantages, mais aussi des inconvénients par rapport aux bases de données relationnelles. 

Pour donner un bref aperçu, les bases de données NoSQL sacrifient certaines caractéristiques des bases de données relationnelles, telles qu'une structure bien définie et des relations strictes entre les entités, afin d'obtenir une mise à l'échelle et une réplication meilleures et plus faciles, afin de traiter de grandes quantités de données, tout en étant généralement plus flexibles, moins chères et plus faciles à gérer. 

MongoDB est spécifiquement une base de données documentaire, qui n'est qu'un type de SGBD NoSQL. (les autres étant les bases de données clé/valeur, colonne, graphe et encaissement). Comme toute chose en ingénierie, il n'y a pas de meilleure ou de pire solution absolue, mais il y a toujours un compromis à faire, selon le contexte. Il n'est pas rare que les applications modernes utilisent plus d'un type de base de données. 

Ainsi, dans cette première tâche, nous allons avoir un aperçu rapide de MongoDB en exécutant nos premières commandes pour explorer, voir notre premier document et ensuite créer notre première base de données. 

* Ouvrir le terminal 

* Démarrer le service MongoDB
```
sudo service mongod start
```
* Vérifier l'état du service 
```
sudo systemctl status mongod
```
Si la commande ci-dessus retourne failed, reconfigurer le port: ```sudo rm -rf /tmp/mongodb-27017.sock```,redémarrer :```sudo service mongod start```et revérifier l'etat du service (```sudo systemctl status mongod```).

* Accéder au Mongo Shell :

```
mongo
```

* Pour l'instant, il s'agit d'une installation récente, mais voyons ce qu'il y a dedans. En utilisant la commande "show dbs", nous pouvons jeter un coup d'œil à la liste des bases de données présentes dans cette instance. 

```
show dbs
```
![image](https://user-images.githubusercontent.com/73080397/212306927-a76dbe4b-1cf7-4da9-b6b6-ce6c1d96a16b.png)

Comme vous pouvez le voir, il y a trois bases de données déjà créées par défaut. Elles sont utilisées par MongoDB lui-même pour stocker les utilisateurs, la configuration et d'autres données.

* En tant que débutants, nous ne sommes pas vraiment concernés par ces bases, mais puisqu'elles sont là et que nous sommes curieux, il n'y a aucun mal à y jeter un coup d'œil. Par exemple, voyons ce qu'il y a dans la BDD admin.

```
use admin
```
![image](https://user-images.githubusercontent.com/73080397/212309121-24589e0e-491a-4072-822b-ed8960068e6f.png)

* L'interpréteur de commandes nous informe qu'il est passé à la base de données admin, et attend d'autres instructions. Afin de voir ce qu'il y a dedans, nous voulons regarder les collections contenues dans la base de données, donc nous tapons :

```
show collections
```
![image](https://user-images.githubusercontent.com/73080397/212309993-24392ade-8b44-49f9-b7ce-6f442d147d2c.png)

Comme vous pouvez le voir, la base de données admin ne contient pour l'instant qu'une seule collection, appelée system.version. 

Une collection, dans la nomenclature NoSQL, est conceptuellement similaire à une table dans les bases de données relationnelles. Cependant, dans le contexte d'une base de données documentaire NoSQL, elle est nommée à juste titre collection, puisqu'il s'agit, en fait, d'une collection de différents documents. 

Nous allons maintenant voir à quoi ressemble un document réel. En dehors des commandes telles que celles que nous avons utilisées jusqu'à présent, "use" et "show", nous pouvons utiliser le JavaScript standard dans le shell MongoDB:

* Écrivons "db.system.version.find()". Donc, nous avons utilisé l'objet db pour accéder à la collection system.version, et, sur cela, nous exécutons la méthode find(), qui, lorsqu'aucun argument n'a été spécifié, renvoie tous les documents disponibles dans la collection. 

```
db.system.version.find()
```
![image](https://user-images.githubusercontent.com/73080397/212310692-44b6dcb5-6b89-4e58-8996-bee04e2d2b4a.png)

* Nous pouvons donc dire en toute confiance que cette collection contient un document. Pour confirmer cela, nous pouvons utiliser une autre méthode appelée "count()". Nous écrivons donc ```db.system.version.count()```, qui renvoie le nombre de documents dans une collection:

![image](https://user-images.githubusercontent.com/73080397/212311611-7ffe5164-1da2-41b5-832a-521aeae49535.png)

 Un document, comme vous pouvez le voir, est très similaire à un objet JSON ordinaire. Le document que nous voyons contient deux champs. Un champ est une construction similaire à une colonne dans une base de données relationnelle, mais nous verrons bientôt que c'est beaucoup plus. Dans ce cas, nous avons un champ `_id`, qui contient une chaîne, FeatureCompatibilityVersion, et un champ appelé `version`, qui contient la chaîne 4.4.
 
 * Maintenant, effaçons le shell en utilisant la commande `cls`
 
 Alors... où en étions-nous ? Si nous ne nous souvenons pas de la base de données sur laquelle nous travaillions, nous pouvons simplement taper `db` pour demander à MongoDB. 
 
 Maintenant, créons une base de données. Pour ce faire, nous pouvons taper `use myFirstDatabase` Ok. MongoDB nous indique qu'il a basculé vers la nouvelle base de données. 
 Cependant, si nous exécutons à nouveau `show dbs`, notre base de données n'est pas listée. C'est parce qu'elle ne contient encore rien. 
 
 ![image](https://user-images.githubusercontent.com/73080397/212314742-8aa5ac25-aa66-41fb-a721-3041aa866e50.png)

 Mais, maintenant, nous allons créer une collection. 
 
 ```
 db.createCollection("myFirstCollection")
 ```
 
 Maintenant, si nous exécutons `show dbs`, nous pouvons voir que notre base de données a été correctement créée. Et si nous exécutons `show collections`, nous pouvons voir que notre première collection a également été créée. 
 
 ![image](https://user-images.githubusercontent.com/73080397/212315634-90ada4dc-a907-46e1-bd79-4c736245e2ca.png)

 
 Maintenant, nous allons effacer le shell à nouveau. 
 
 Félicitations ! Vous venez d'explorer votre première instance, base de données et collection MongoDB. Vous avez eu un aperçu de ce qu'est un document et vous avez créé votre première base de données et votre première collection. Dans notre prochaine tâche, nous allons créer notre premier document.

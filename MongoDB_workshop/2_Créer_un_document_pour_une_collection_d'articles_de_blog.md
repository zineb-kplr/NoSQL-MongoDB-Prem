# 2. Créer un document pour une collection d'articles de blog 

Dans cette tâche, nous allons créer notre premier document. Donc, assurons-nous que nous sommes toujours sur la même page que la tâche précédente. 

* En exécutant `db`, vous devriez toujours être dans myFirstDatabase. 

* Si ce n'est pas le cas, vous vous souvenez peut-être de la tâche précédente et que vous pouvez exécuter la commande `use myFirstDatabase`

* En effet, nous allons apprendre à supprimer une base de données, puisque nous ne l'utiliserons plus à l'avenir. 

```
db.dropDatabase()
```
* Comme vous pouvez le voir, MongoDB nous confirme que l'opération a réussi. Maintenant, jetons à nouveau un coup d'oeil aux bases de données. 

```
show dbs
```

![image](https://user-images.githubusercontent.com/73080397/212318342-1e1ebfbe-552c-4dd4-8066-793cfcf55fb5.png)

Ainsi, notre première base de données a été correctement supprimée.

Et maintenant, commençons notre premier document. Pour ce projet, nous voulons stocker des articles de blog:

* Créons une base de données pour notre blog. 

```
use blog
```

* Maintenant nous allons utiliser la méthode insert() pour une collection de billets. Comme cette collection n'existe pas, MongoDB va la créer pour nous:

```js
db.posts.insert({
	title: 'MongoDB rules',
	body: 'My First MongoDB document',
	date: ISODate('2023-03-30T18:30:00Z'),
	tags: ['mongodb', 'databases'],
	likes: 2,
	author: {
		name: 'Douaâ',
		surname: 'Hayel'
	},
	location: {
		type: 'Point',
		coordinates: [-112.45, 37.76]
	}
})
```
Un message est affiché : `WriteResult({ "nInserted" : 1 })`

* Effaçons le shell `cls`
* Retrouvons le document:
```
db.posts.find()
```

![image](https://user-images.githubusercontent.com/73080397/212322929-6e602425-4084-41d3-9175-34253ccc1de3.png)

Comme vous pouvez le voir, MongoDB a ajouté un champ pour nous, qui s'appelle `_id`. Il s'agit d'un identifiant unique de notre document. Si nous l'avions voulu, nous aurions pu passer outre en ajoutant un champ `_id` à notre propre document, lors de son insertion, avec une clé primaire qui aurait pu avoir un sens pour nous. 

Nous avons donc appris comment lancer notre premier document et certains des types de données que MongoDB gère, comme les chaînes de caractères, les tableaux de dates et les entiers, les documents intégrés et les GeoJSON. Donc, dans la prochaine tâche, nous allons commencer à interroger notre base de données et à mettre à jour les documents.


 

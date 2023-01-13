# 3.Requêtes et mise à jour de documents

Dans cette tâche, nous allons commencer à interroger la base de données et apprendre à mettre à jour un document. 

* Ajoutons un deuxième document dans notre collection posts:

```js
db.posts.insert({
	likes: 5,
	title: 'Second Post',
	author: {
		name: 'Zineb',
		surname: 'Zannouti'
	},
	body: 'Body of our second post',
	date: ISODate('2023-03-30T03:00:00Z')
})
```
* Vérifier le document:
```
db.posts.find().pretty()
```

![image](https://user-images.githubusercontent.com/73080397/212326626-7e907689-ba2e-45cd-acfd-01e530c2f2f5.png)

Comme vous pouvez le voir, nous avons maintenant les deux documents stockés. De plus, notre deuxième document n'a pas de *tags* ni de *location*. De plus, l'ordre des champs n'a pas d'importance. Ceci est dû au fait que MongoDB est *schema-less*. Cela signifie que nous n'avons pas eu à définir un schéma pour contraindre la forme de tout ce qui est stocké dans le système. Si vous êtes familier avec les bases de données relationnelles, cela peut sembler étrange. Cependant, c'est l'une des raisons pour lesquelles NoSQL est si puissant à l'échelle. 

* Maintenant, disons que nous voulons trouver notre deuxième article. Pour ce faire, nous pouvons utiliser la méthode `find()` et chercher par son titre. C'est ce qu'on appelle communément l'interrogation de la base de données. 

```
db.posts.find({title: 'Second Post'}).pretty()
```
![image](https://user-images.githubusercontent.com/73080397/212328406-da181af8-e3fd-4f3b-8829-bcca53675ab2.png)

* trouver tous les documents et ensuite les trier par le champ title dans l'ordre ascendant (-1 pour l'ordre descendant):
```
db.posts.find().sort({title: 1}).pretty()
```

![image](https://user-images.githubusercontent.com/73080397/212329383-6eb0fd58-9cd8-4372-86c6-828042010c60.png)


* Trouver tous les posts qui ont plus de deux likes en utilisant `gt` (greater than) 
```
db.posts.find({likes: {$gt: 2}}).pretty()
```

* Trouver tous les posts qui ont au moins deux likes en utilisant `gte` (greater than or equal)
```
db.posts.find({likes: {$gte: 2}}).pretty()
```

* Trouver tous les posts qui ont au moins deux likes en utilisant `gte` (greater than or equal) et les trier par ordre descendant des nombres de likes :
```
db.posts.find({likes: {$gte: 2}}).pretty().sort({like: -1}).pretty()
```

Lisez : [Opérateurs Logiques et opérateurs de comparaison dans MongoDB](https://kinsta.com/fr/blog/operateurs-mongodb/)




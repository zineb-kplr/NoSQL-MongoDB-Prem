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

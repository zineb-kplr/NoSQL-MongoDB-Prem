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

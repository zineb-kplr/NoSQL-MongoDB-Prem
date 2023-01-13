# 4.Insertion et mise à jour de plusieurs documents à la fois

 Dans cette tâche, vous allez apprendre comment insérer et mettre à jour plusieurs documents à la fois. Il existe une commande shell, appelée `insertMany`, qui vous permet d'insérer plus d'un document à la fois. Cette commande accepte un tableau d'objets :
 
 ```js
 
db.posts.insertMany(
	[
		{
			title: 'Awsome Post',
			body: 'Body of Awsome Post',
			date: ISODate('2023-03-30T03:30:00Z')
		},
		{
			title: 'Awsome Post',
			body: 'Body of Awsome Post number 2',
			likes: 3,
			date: ISODate('2025-03-30T02:30:00Z'),
			location: {
				type: 'Point',
				coordinates: [-97,74, 30.27]
			}
		}
	]
	)
```

![image](https://user-images.githubusercontent.com/73080397/212361622-360c98bc-226b-467b-bd83-eeff5b99f17b.png)

Comme vous pouvez le voir, MongoDB nous a confirmé que les deux documents ont été stockés.

Disons que nous voulons mettre à jour tous les articles de blog, avec un booléen `published`, pour determiner si l'article a été publié ou non.

```js
db.posts.update(
	{},
	{
		$set: {
			published: false
		}
	}
)
```
![image](https://user-images.githubusercontent.com/73080397/212364058-e98c2b66-97d2-44ee-8436-a7660c525805.png)

Comme vous pouvez le voir. Nous avons 4 documents dans notre base de données de blog, mais le writeResult ici dit qu'un seul a été trouvé et qu'un seul a été modifié. 

Que se passe-t-il ? C'est parce que la commande `update`, par défaut, met à jour un seul document. Dans ce cas, elle n'a mis à jour que le premier document qu'elle a trouvé. Pour savoir lequel, nous pouvons rechercher les documents qui contiennent effectivement ce champ : nous pouvons le faire en utilisant l'opérateur `$exists`:

```js
db.posts.find(
		{
			published: {
				$exists: true
			}
		}
	).pretty()
```

![image](https://user-images.githubusercontent.com/73080397/212365062-e3841017-99ef-48b4-83b8-7c556c60c0e7.png)

Maintenant, nous aimerions réparer cela. Nous voulons mettre à jour tous les documents en même temps. Pour ce faire, nous devons spécifier des options pour notre méthode de mise à jour. 
```js
db.posts.update(
	{},
	{
		$set: {
			published: false
		}
	},
	{multi: true}
)
```
![image](https://user-images.githubusercontent.com/73080397/212366810-11e2b3ee-9d75-4864-9fef-60fcd6aafd98.png)

Maintenant c'est beaucoup mieux. Il dit qu'il a fait correspondre 4 documents, et qu'il a modifié 3 documents. C'est parce que, bien sûr, l'un de nos documents avait déjà le champ publié à false.

* Retrouver nos deux postes portant le même titre :
```
db.posts.find({title: 'Awsome Post'})
```
![image](https://user-images.githubusercontent.com/73080397/212367515-ea8e3a18-bf0b-42ef-8571-187fa9cc9b46.png)

* Trouver le seul article qui a le champ "likes".

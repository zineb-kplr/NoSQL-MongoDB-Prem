# 7.créer un index unique et un index 2dsphere pour les requêtes géographiques 

Dans cette tâche, nous allons créer deux autres types d'index et examiner leurs avantages. 

* Aller dans la BDD *posts* 

Compte tenu de l'importance des index lors de la mise à l'échelle des applications, nous souhaitons ajouter un index à notre champ titre. 

* Allons donc dans la section Indexe > Create Index > nom : "title" > Sélectionner le champ title > Selectionner index ascendant > Selectionner la première option "Créer un index unique" > Create index

![image](https://user-images.githubusercontent.com/73080397/213517395-799739db-4e73-4a5e-bc31-dec34892bbce.png)

L'utilisation de cette option signifie que nous ne voulons pas de doublons dans notre champ. Dans notre cas, nous ne voulons pas d'articles de blog ayant le même titre dans notre base de données. C'est déjà le cas pour le champ ```_id``` que MongoDB crée automatiquement.

![image](https://user-images.githubusercontent.com/73080397/213518225-5b338ebb-199e-4c96-a61f-73f77f9067f6.png)

Nous recevons une erreur qui indique que la construction de l'index a échoué parce que nous avons un doublon. En particulier, elle dit que nous avons plus d'un titre avec le titre "Awesome Post", donc nous allons corriger cela:

* Cliquer sur Cancel
* Nous retournons dans la section Documents, et trouvons le dernier document avec le titre "Awesome Post". Nous pouvons le modifier en double-cliquant sur la chaîne de caractères, et le remplacer par le titre ```Most Awesome post```:

![image](https://user-images.githubusercontent.com/73080397/213519533-05d4b266-8f0b-4c07-84da-84886bf9a4de.png)

* Cliquer sur Update
* Retourner à la section Indexes et recréer l'index :

![image](https://user-images.githubusercontent.com/73080397/213520909-a494dfd2-5fc9-4cb1-92ad-42575b405267.png)

![image](https://user-images.githubusercontent.com/73080397/213521300-58b105bf-139c-46a8-aca0-ebbb3e9e10aa.png)

Et voilà, notre index a été créé avec succès!

* Maintenant, nous pouvons aller dans notre section Plan d'exploration, et ensuite nous écrivons notre requête dans le champ de texte du filtre. 
```js
{title: 'Awsome Post'}
```
![image](https://user-images.githubusercontent.com/73080397/213521964-d6013e49-9fec-4217-9ab4-af8b7bb7934c.png)

* Retourner dans la collection **posts_big** > Analyse > Aller dans le champs **location** > Zoomer sur la carte jusqu'à faire apparaître les points séparés 
* Cliquer sur Draw a circle et entourer un point d'un cercle pour faire apparaître le filtre de localisation:

![image](https://user-images.githubusercontent.com/73080397/213550926-986a2c53-3984-4de6-8c5e-88f04a30528c.png)

Aller dans Explain Plan > Explain 

![image](https://user-images.githubusercontent.com/73080397/213551375-d6e51fad-f782-4d81-8dca-cc7eb76d4e56.png)

Comme vous pouvez le voir, cela prend 7,5 secondes, dans mon cas, il s'agit d'un balayage de collection sur 5 millions de documents.

Comme vous pouvez le deviner, nous pouvons créer un index ici aussi. Plus important encore, nous pouvons créer un index adapté aux données géographiques. 

* Indexes > Create index > index fields: location et type 2dsphere > create index

![image](https://user-images.githubusercontent.com/73080397/213551993-4c8e190f-78ee-4266-bf12-cbc5f0f6df7e.png)

* Explain plan > Explain 

![image](https://user-images.githubusercontent.com/73080397/213552895-f0044c3f-6249-4458-a5a2-d91f28009d60.png)


 Comme vous l'avez peut-être deviné, tout fonctionne maintenant beaucoup plus vite. C'est génial !
 
 Fin du workshop


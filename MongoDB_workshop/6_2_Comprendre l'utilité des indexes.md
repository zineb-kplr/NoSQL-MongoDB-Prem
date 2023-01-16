# 6.2.Comprendre l'utilité des indexes

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

Vous pouez remarquer la création de la collection **posts_big** 

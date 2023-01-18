# Installer MongoDB sur Ubuntu

La version de Ubuntu : ```cat /etc/os-release```

![image](https://user-images.githubusercontent.com/73080397/212052665-cc4f0f36-47f7-47ae-87e4-cd1026989cd0.png)

Pour cette version, l'installation comme décrite dans la documentation officielle de MongoDB retourne des erreurs dus au manque de quelques packages. (dernière vérification 12/01/2023).

```
sudo apt install dirmngr gnupg apt-transport-https ca-certificates software-properties-common
```

```
echo "deb http://security.ubuntu.com/ubuntu impish-security main" | sudo tee /etc/apt/sources.list.d/impish-security.list
```

Aller dans root user :

```
root -i
```

Coller la commande :
```
wget http://archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2_amd64.deb
```

Toujour dans le root user, coller:

```
dpkg -i libssl1.1_1.1.1f-1ubuntu2_amd64.deb
```

```
apt update
apt install libssl1.1
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list
apt update
apt install -y mongodb-org
```


Télecharger MongoDB Compass
```
wget https://downloads.mongodb.com/compass/mongodb-compass_1.35.0_amd64.deb
```

Installer MongoDB Compass
```
sudo dpkg -i mongodb-compass_1.35.0_amd64.deb
```

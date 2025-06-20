# Cas pratique
## J'exécute mon 1er conteneur


1. Installer docker for windows
2. Installer l'extension docker for vscode

>Cette extension permettra à votre IDE d'interagir avec le moteur docker, vous pouvez gérer vos images, vous connectez à un registre ou encore démarrer un conteneur à partir d'un image.

3. Demander à Claude :

>écris une petite application web de test qui devra fonctionner dans un conteneur, le service doit écouter sur toutes les interfaces réseau afin que je puisse y accèder depuis mon poste avec une redirection de port

4. Pour lister les images présentes sur votre poste vous pouvez lancer la commande  :

```bash
docker images
```

6. lancer le build de l'image depuis VSCode :

Faire un clic droit sur le Dockerfile -> Build image

ou bien en ligne de commande (en étant placé dans votre projet, il faut que le Dockerfile soit présent)

```bash
# Build
docker build -t app:1.0 . # -t app:1.0 permet de taguer directement votre image avec le nom app et le tag 1.0
```

Si vous n'avez pas utilisé le paramètre -t vous pourrez toujours taguer avec la commande (après le build réussi) :

```bash
docker images #pour récupérer l'id de l'image à taguer
docker tag ID_IMAGE app:1.0 #remplacer ID_IMAGE par l'id récupéré avec la commande docker images
```

>ATTENTION: si on ne précise pas de tag, docker taguera automatiquement l'image avec **latest**

7. vous pouvez maintenant démarrer votre conteneur depuis votre image fraichement créée

En ligne de commande :

```docker run -p PORT:TARGET_PORT IMAGE_NAME:TAG```

|||
|-|-|
|**PORT** | correspond au port qu'utiliseront les utilisateurs dans leur navigateur |
|**TARGET_PORT** | il s'agit du port exposé par votre application |(ligne EXPOSE de votre Dockerfile)

Exemple :

```bash
# Run avec redirection de port
docker run -p 8080:80 app:1.0
```

>Ici on instancie l'image **app:1.0** dans un conteneur en prenant soin d'indiquer la redirection de port : on accédera au port 8000 depuis le navigateur et docker transférera les requetes sur le port 80 qui est le port exposé par votre application.


## Vers un registre exterieur
### Connecter le registre d'images dans VSCode

1. Cliquer sur l'icone de l'extension Docker et dans la partie Registries cliquer sur "Connect Registry..."
2. Choisissez "Generic Registry V2"
3. saisir : https://kregistry.ddns.net/default
4. les identifiants de connexion et valider

Quand vou avez branché un registre extérieur vous allez pouvoir ypousser une image. Pour cela nous allons taguer l'image comme suit :

```bash
docker images
docker tag IMAGE_ID REGISTRY/PROJECT_NAME/IMAGE_NAME:TAG
```

|||
|-|-|
**IMAGE_ID** | ID de l'image à envoyer|
**REGISTRY** | adresse du registre (sans https://)|
**PROJECT_NAME** | projet dans le registre, nous avions vu ici "/default"|
**IMAGE_NAME** | le nom de votre image|
**TAG** | le tag|

Ce qui donnera dans notre exemple :

```bash
docker image
docker tag f068bc204a0e kregistry.ddns.net/default/app:1.0
```

Une fois l'image tagué elle est prête à être envoyée sur le registre :

```bash
docker push kregistry.ddns.net/default/app:1.0
```
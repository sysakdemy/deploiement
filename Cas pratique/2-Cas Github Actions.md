# Sur votre poste de travail
## Initialisation de votre projet git

1. Ajouter dans votre projet un répertoire .github/workflows
2. Dans ce répertoire ajouter le fichier docker-image.yml
3. Se connecter sur votre Github
4. Créer un projet vide avec le nom de votre projet local
5. Dans VSCode initialiser le projet git : onglet "Source control" dans le panneau latéral gauche
6. Indexer tous les fichiers du projet en cliquant sur le + à droite de "Changes"
7. Ecrire un message de commit

# Sur le site Github.com
## Configuration de Github Actions dans votre projet

1. Sur Github créer la coquille vide de votre projet

2. Revenir sur votre poste et passer la commande suivante :
```
git remote add origin https://github.com/..../projet
```

3. Revenir sur la page de votre projet sur Github
4. Settings > Secrets and variables > Actions
5. Créer un nouveau secret "New repository secret"
6. Name : **GCP_SA_KEY**
7. Valeur : coller le contenu de key.json, vous pouvez le récupérer ici http://bit.ly/44mD5pW
8. Settings > Secrets and variables > Actions
9. Onglet Variables cliquer sur **New repository variable**
10. Name: **REGISTRY**
11. Value : **europe-west3-docker.pkg.dev/helpful-mode-462809-b9/default**

Cette configuration va permettre à Github Action de comprendre les variables présentes dans votre docker-image.yml :

La variable REGISTRY va indiquer l'adresse de votre registre d'image 

```
REGISTRY: ${{ vars.REGISTRY }}
```

Le secret GCP_SA_KEY va permettre l'authenfication de Github Action à votre registre d'image

```
${{ secrets.GCP_SA_KEY }}
```

> Ce fichier docker-image.yml est réutilisable pour tous vos projets

Une fois la configuration terminée vous allez pouvoir pousser vos modification sur votre Github avec le bouton "Syncrhonize" ou avec la commande :

```
git push -u origin main
```

# Cas pratique

1. Installer docker for windows
2. Installer l'extension docker for vscode

4. Demander à Claude :

>écris une petite application web de test qui devra fonctionner dans un conteneur, le service doit écouter sur toutes les interfaces réseau afin que je puisse y accèder depuis mon poste avec une redirection de port

5. lancer la commande 

```bash
docker images
```

6. lancer le build de l'image depuis VSCode :

Faire un clic droit sur le Dockerfile -> Build image

ou bien en ligne de commande :

```bash
# Build
docker build -t app .
```

7. relancer la commande du point n°5 (docker images) et normalement vous voyez également votre image dans l'extension Docker de VSCode.

8. vous pouvez maintenant démarrer votre conteneur depuis votre image fraichement créée :

```bash
# Run avec redirection de port
docker run -p 8080:80 app
```

## Vers un registre exterieur
### Connecter le registre d'images dans VSCode

1. Cliquer sur l'icone de l'extension Docker et dans la partie Registries cliquer sur "Connect Registry..."
2. Choisissez "Generic Registry V2"
3. saisir : https://kregistry.ddns.net/default
4. les identifiants de connexion et valider

Ce registre est pour le moment vide.
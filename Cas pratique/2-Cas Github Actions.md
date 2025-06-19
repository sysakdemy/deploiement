# Configuration de Github Actions dans votre projet

1. Ajouter dans votre projet un répertoire .github/workflows
2. Dans ce répertoire ajouter le fichier docker-image.yml

3. Se connecter sur votre Github
4. Créer un projet vide
5. Settings > Secrets ans variables > Actions
6. Créer un nouveau secret "New repository secret"
7. Name : GCP_SA_KEY
8. Valeur : coller le contenu de key.json
9. Settings > Secrets ans variables > Actions
10. Onglet Variables "New repository variable"
11. Name: REGISTRY
12. Value : europe-west3-docker.pkg.dev/helpful-mode-462809-b9/default

Vous pouvez ensuite commit et pousser les modifications de votre projet local sur votre Github
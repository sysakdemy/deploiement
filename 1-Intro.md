## Table of Contents

- [Le déploiement](#le-déploiement)
- [Introduction aux infrastructures de déploiement (cloud, on-premise, hybride)](#introduction-aux-infrastructures-de-déploiement-cloud-on-premise-hybride)
  - [Infrastructure cloud](#infrastructure-cloud)
  - [Infrastructure on-premise](#infrastructure-on-premise)
  - [Infrastructure hybride](#infrastructure-hybride)

# Le déploiement

Un déploiement c'est l’ensemble des opérations nécessaires pour rendre une application, un service, ou un système accessible et fonctionnel dans un environnement donné. Cela peut être en production ou en test.

- transfert du code, 
- l'installation des dépendances,
- la configuration,
- la mise en réseau.

Il existe différentes méthodes de déploiement

- Manuel : un administrateur réalise toutes les étapes de mise en ligne à la main
- Automatisé : avec des outils comme par exemple Ansible, Gitlab CI/CD, Github Action
- Déploiement Continu : chaque modification est poussée automatiquement sur l'environnement ciblé, avec par exemple Gitlab CI/CD, Github Action, Jenkins

# Introduction aux infrastructures de déploiement (cloud, on-premise, hybride)

Les infrastructures de déploiement représentent l'architecture technique sur laquelle les applications et services sont hébergés et exécutés. Avec l'évolution des technologies informatiques, différentes approches se sont développées, chacune avec ses avantages et contraintes spécifiques.

## Infrastructure cloud
Le cloud computing offre des ressources informatiques à la demande via internet, sans nécessiter d'investissement direct dans du matériel physique.
Caractéristiques principales :

* Élasticité et mise à l'échelle automatique
* Modèle de paiement à l'usage
* Maintenance gérée par le fournisseur
* Accessibilité mondiale

Types de services cloud :

* IaaS (Infrastructure as a Service) : AWS EC2, Google Compute Engine : on loue une machine virtuelle et on gére tout sauf la partie physique, stockage et réseau.
* CaaS (Container as a Service) : GKE, EKS, AKS) : on déploie et on fait évoluer nos conteneurs sur une infrastructure dédiée
* PaaS (Platform as a Service) : Azure App Service, Google App Engine : on déploie notre code
* SaaS (Software as a Service) : Salesforce, Microsoft 365 : on ne fait qu'utiliser l'application en ligne.

📊 Comparaison

| Modèle |	Tu fournis... |	Fournisseur fournit... |	Tu contrôles... |
|--------|----------|---------|--------|
|IaaS	|OS, apps|	VM, réseau, stockage	|Tout sauf le matériel |
|CaaS	|Conteneurs|	Infra + orchestration (K8s)|	Déploiement de tes apps|
|PaaS	|Code/app	|Tout le reste|	Peu de choses (pas l’infra)|
|SaaS|	Rien (juste un compte)|	Tout	|Juste l’usage|



## Infrastructure on-premise
L'infrastructure on-premise (sur site) désigne les ressources informatiques hébergées et gérées dans les locaux de l'entreprise.

Caractéristiques principales :

* Contrôle total sur l'infrastructure
* Sécurité physique directe
* Conformité réglementaire facilitée
* Coûts initiaux élevés mais prévisibles

Composants typiques :

* Centres de données privés
* Serveurs physiques et virtuels
* Équipements réseau
* Systèmes de stockage dédiés

## Infrastructure hybride
L'approche hybride combine les infrastructures cloud et on-premise pour tirer parti des avantages de chaque modèle.

Caractéristiques principales :

* Flexibilité accrue
* Optimisation des coûts
* Transition progressive vers le cloud
* Répartition stratégique des charges de travail

Scénarios courants :

* Applications critiques sur site et charges variables dans le cloud
* Cloud bursting (débordement vers le cloud en cas de pic d'activité)
* Reprise après sinistre dans le cloud
* Conservation des données sensibles en local

Critères de choix
Le choix entre ces différentes infrastructures dépend de plusieurs facteurs :

* Nature des applications et des données
* Exigences de performance et de latence
* Contraintes budgétaires et financières
* Compétences techniques disponibles
* Réglementations et conformité

La tendance actuelle s'oriente vers des architectures hybrides et multi-cloud, permettant une plus grande souplesse et résilience face aux évolutions technologiques et aux besoins métiers.
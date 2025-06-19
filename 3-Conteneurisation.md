## Table of Contents

- [Conteneurs vs VM](#conteneurs-vs-vm)
  - [🐳 Conteneurs vs 🖥️ Machines Virtuelles (VM)](#-conteneurs-vs-️-machines-virtuelles-vm)
- [Concepts clés : conteneurisation, orchestration, scalabilité](#concepts-clés--conteneurisation-orchestration-scalabilité)
  - [La conteneurisation](#la-conteneurisation)
    - [Moteurs de conteneurs](#moteurs-de-conteneurs)
    - [Ecosystème Docker](#ecosystème-docker)
    - [Orchestration](#orchestration)
      - [Fonctionnalités principales](#fonctionnalités-principales)
  - [Plateformes d'orchestration](#plateformes-dorchestration)
    - [Concepts Kubernetes](#concepts-kubernetes)
      - [Scalabilité](#scalabilité)
    - [Technologies et patterns](#technologies-et-patterns)
  - [Considérations importantes](#considérations-importantes)
    - [Interconnexion de ces concepts](#interconnexion-de-ces-concepts)


# Conteneurs vs VM

## 🐳 Conteneurs vs 🖥️ Machines Virtuelles (VM)

La virtualisation, c’est une technique qui permet de faire fonctionner plusieurs systèmes (ou machines virtuelles) sur un seul ordinateur physique.

La conteneurisation est une méthode de virtualisation au niveau du système d'exploitation qui permet d'empaqueter une application et ses dépendances dans un environnement isolé appelé conteneur.

| Critère	| Conteneurs | Machines Virtuelles |
| ------- | ---------- | ------------------- |
| Isolation |	Processus isolés partageant le noyau Linux |	Systèmes complets avec leur propre OS |
| Système d'exploitation |	Partagent le noyau de l’hôte |	Chaque VM a son propre noyau (hyperviseur) |
| Légèreté |	Très légers, démarrage rapide | Plus lourds, démarrage plus lent |
| Performances |	Presque natives	| Légère surcouche due à la virtualisation |
| Taille |	Quelques Mo à centaines de Mo |	Plusieurs Go (OS complet inclus) |
| Utilisation typique |	Microservices, CI/CD, déploiement rapide |	Isolation forte, compatibilité OS, legacy |


![](conteneurs-vs-vms.png)


*Le noyau est le coeur du système d'exploitation Linux c'est lui qui va gérer les ressources, les accès aux fichiers etc... c'est un peu le chef d'orchestre.*

# Concepts clés : conteneurisation, orchestration, scalabilité

## La conteneurisation

Tous les fichiers nécessaires à l'exécution sont fournis dans une image 

Une image contient les fichiers qui forment votre système de fichiers et les metadata :

    l'auteur de l'image,
    la commande a exécuter dans le conteneur lors de son démarrage,
    des variables d'environnement,
    etc.


**Principes fondamentaux**

✅ **Isolation** : Les conteneurs fonctionnent de manière isolée tout en partageant le même noyau OS

✅ **Portabilité** : Les applications conteneurisées s'exécutent de manière identique quel que soit l'environnement

✅ **Légèreté** : Contrairement aux machines virtuelles, les conteneurs ne nécessitent pas d'OS complet

✅ **Rapidité** : Démarrage et arrêt en quelques secondes

Ils sont bien plus rapides à mettre en oeuvre pour de la mise en production ou du développement.


**Avantages**

* Environnements de développement cohérents : Les conteneurs garantissent que l'application se comporte de manière identique, du développement à la production, éliminant les problèmes de "ça marche sur ma machine".
* Déploiements prévisibles : Ils simplifient le processus de déploiement en s'assurant que toutes les dépendances sont incluses, réduisant ainsi les erreurs et les imprévus.
* Utilisation efficace des ressources : Les conteneurs partagent le noyau du système d'exploitation hôte, ce qui permet une utilisation plus efficiente du matériel par rapport aux machines virtuelles.
* Isolation des applications : Chaque application fonctionne dans un environnement isolé, empêchant les conflits de dépendances et augmentant la sécurité.

### Moteurs de conteneurs

* **Docker** : Plateforme leader pour créer, distribuer et exécuter des conteneurs

* **Podman** : Alternative à Docker

* **Containerd** : Runtime de conteneur utilisé par Docker et Kubernetes


### Ecosystème Docker

Plongeons dans les composants clés qui forment l'épine dorsale de la conteneurisation avec Docker, une plateforme essentielle pour le développement, le déploiement et la gestion d'applications conteneurisées.

**Images** : Une image Docker est un modèle léger, autonome et exécutable qui inclut tout ce dont une application a besoin pour fonctionner : le code, un runtime, des bibliothèques système, des outils système et des paramètres.Elle est construite à partir d'un Dockerfile, un fichier texte qui contient toutes les commandes nécessaires pour assembler l'image. Les images sont immuables et servent de base pour créer des conteneurs.

**Conteneur**
Un conteneur est une instance en cours d'exécution d'une image. C'est un processus isolé qui s'exécute sur l'hôte avec ses propres espaces de noms (réseau, système de fichiers, processus).

**Dockerfile**
Un Dockerfile est un fichier texte contenant les instructions pour construire une image Docker. Il définit étape par étape comment assembler l'environnement.

**Registry**
Un registry est un service de stockage et de distribution d'images Docker. Docker Hub est le registry public par défaut, mais on peut avoir des registries privés.

> Démo

### Orchestration

L'orchestration de conteneurs permet d'automatiser le déploiement, la gestion, la mise à l'échelle des conteneurs.

Le développeur n'a plus à se soucier de toute la partie infrastructure, réclamer du stockage ou encore des accès réseau à ses copains de l'infra.

![](infra-k8s.png)

#### Fonctionnalités principales

* **Placement** : Distribution intelligente des conteneurs sur les nœuds disponibles
* **Autorestart** : Redémarrage automatique des conteneurs défaillants
* **Service discovery** : Localisation des services dans un cluster dynamique
* **Load balancing** : Répartition du trafic entre plusieurs instances
* **Mises à jour progressives** : Déploiements sans interruption de service

## Plateformes d'orchestration

* **Kubernetes** : Standard pour l'orchestration à grande échelle
* **Docker Swarm** : Solution intégrée à l'écosystème Docker
* **Amazon ECS** : Service d'orchestration géré par AWS
* **Nomad** : Orchestrateur multi-technologie de HashiCorp

### Concepts Kubernetes

* **Pods** : Unité d'exécution de base regroupant un ou plusieurs conteneurs
* **Deployments** : Déclarations d'état souhaité pour les applications
* **Services** : Exposition des applications sur le réseau
* **ConfigMaps/Secrets** : Gestion des configurations et données sensibles
* **Namespaces** : Séparation logique des ressources dans un cluster

#### Scalabilité
La scalabilité est la capacité d'un système à s'adapter à une charge croissante en augmentant ses ressources.
Types de scalabilité

* **Verticale (Scale up)** : Augmentation des ressources d'une instance (CPU, RAM)
* **Horizontale (Scale out)** : Ajout d'instances supplémentaires
* **Automatique** : Ajustement dynamique basé sur des métriques prédéfinies
* **Manuelle** : Ajustement déclenché explicitement par un opérateur

### Technologies et patterns

* **Auto-scaling groups** : Mécanismes automatisés d'ajustement du nombre d'instances
* **Stateless design** : Conception d'applications sans état pour faciliter la réplication
* **Microservices** : Architecture permettant de mettre à l'échelle des composants indépendamment
* **Serverless** : Abstraction de l'infrastructure avec mise à l'échelle automatique

## Considérations importantes

* Métriques de déclenchement : CPU, mémoire, latence, requêtes par seconde
Élasticité : Capacité à s'adapter rapidement dans les deux sens (augmentation/diminution)
* Cohérence des données : Synchronisation entre instances lors de la mise à l'échelle
* Répartition géographique : Distribution sur plusieurs régions pour la résilience

### Interconnexion de ces concepts
Ces trois concepts sont profondément liés dans les architectures modernes :

La conteneurisation fournit l'unité de base portable et isolée
L'orchestration gère le cycle de vie et les interactions entre conteneurs
La scalabilité permet au système d'évoluer en fonction des besoins

Ensemble, ils forment le socle des infrastructures cloud-natives, permettant des déploiements rapides, fiables et adaptables aux charges variables.
# 🐳 Guide Complet sur Docker

Bienvenue dans ce guide de base sur Docker. Il couvre les principaux concepts que tout développeur ou administrateur système devrait connaître : **images**, **conteneurs**, **Dockerfile**, **Docker Compose**, **volumes**, **réseaux** et **Swarm**.

---

## 📦 1. Docker Image

Une **image Docker** est un modèle figé qui contient tout ce dont une application a besoin pour s'exécuter (code, dépendances, configuration système, etc.).

### 🔧 Commandes utiles

#### Télécharger une image existante depuis Docker Hub
```bash
docker pull nginx
```

#### Lister les images disponibles localement
```bash
docker images
```
#### Supprimer une image
```bash
docker rmi <image_id>
```
##🧱 2. Docker Container
Un conteneur est une instance en cours d’exécution d’une image. Il est isolé mais peut interagir avec le système hôte via des ports, des volumes, etc.


### 🔧 Commandes utiles
```bash
# Lancer un conteneur
docker run -d -p 8080:80 --name mon-nginx nginx

# Lister les conteneurs actifs
docker ps

# Lister tous les conteneurs (y compris stoppés)
docker ps -a

# Arrêter un conteneur
docker stop mon-nginx

# Supprimer un conteneur
docker rm mon-nginx
```
##📝 3. Dockerfile
Un Dockerfile permet de créer des images personnalisées à partir d’instructions textuelles.

###🧪 Exemple de Dockerfile
```bash
# Utiliser une image de base
FROM node:20

# Définir le répertoire de travail
WORKDIR /app

# Copier les fichiers dans l'image
COPY . .

# Installer les dépendances
RUN npm install

# Commande par défaut au démarrage
CMD ["npm", "start"]
```
### 🔧 Commande de build
```bash
docker build -t mon-app .
```
##⚙️ 4. Docker Compose
Docker Compose permet de gérer des applications multi-conteneurs via un seul fichier docker-compose.yml.

###🧪 Exemple de docker-compose.yml
```bash
version: '3.8'

services:
  web:
    build: .
    ports:
      - "3000:3000"
    volumes:
      - .:/app

  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: exemple
```
### 🔧 Commandes utiles
```bash
# Démarrer les services
docker-compose up

# Démarrer en arrière-plan
docker-compose up -d

# Arrêter les services
docker-compose down
```
##💾 5. Docker Volume
Les volumes permettent de persister les données indépendamment du cycle de vie des conteneurs.

### 🔧 Commandes utiles
```bash
# Créer un volume
docker volume create mes-donnees

# Lister les volumes
docker volume ls

# Utiliser un volume dans un conteneur
docker run -v mes-donnees:/data busybox

# Supprimer un volume
docker volume rm mes-donnees
```
##🌐 6. Docker Network
Les réseaux Docker permettent aux conteneurs de communiquer entre eux, en toute sécurité.

###🔧 Commandes utiles
```bash
# Créer un réseau
docker network create mon-reseau

# Lister les réseaux
docker network ls

# Attacher un conteneur à un réseau
docker run -d --network=mon-reseau --name serveur nginx

# Connecter un conteneur existant
docker network connect mon-reseau mon-conteneur
```
##⚓ 7. Docker Swarm
Docker Swarm est l’outil d’orchestration natif de Docker. Il permet de gérer un cluster de nœuds pour le déploiement d’applications distribuées.

###🔧 Commandes utiles
```bash
# Initialiser le swarm
docker swarm init

# Ajouter un nœud (sur une autre machine)
# Affiche une commande avec un token à utiliser

# Déployer un service
docker service create --name web -p 80:80 nginx

# Lister les services
docker service ls

# Mettre à l’échelle un service
docker service scale web=3

# Arrêter un service
docker service rm web
```
---

## 🧠 Exercice pratique : Déployer une application Node.js + PostgreSQL avec Docker

### 🎯 Objectif

Créer un projet Docker complet avec une application Node.js connectée à une base de données PostgreSQL. L'application devra être conteneurisée, isolée en réseau, et persister ses données avec des volumes.

---

### 📝 Étapes à suivre

#### 1. Crée la structure suivante :




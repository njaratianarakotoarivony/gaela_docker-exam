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
## 🧱 2. Docker Container

Un conteneur est une instance en cours d’exécution d’une image. Il est isolé mais peut interagir avec le système hôte via des ports, des volumes, etc.


### 🔧 Commandes utiles

#### Lancer un conteneur
```bash
docker run -d -p 8080:80 --name mon-nginx nginx
```
#### Lister les conteneurs actifs
```bash
docker ps
```
#### Lister tous les conteneurs (y compris stoppés)
```bash
docker ps -a
```
#### Arrêter un conteneur
```bash
docker stop mon-nginx
```
#### Supprimer un conteneur
```bash
docker rm mon-nginx
```
## 📝 3. Dockerfile

Un Dockerfile permet de créer des images personnalisées à partir d’instructions textuelles.

### 🧪 Exemple de Dockerfile

#### Utiliser une image de base
```bash
FROM node:20
```
#### Définir le répertoire de travail
```bash
WORKDIR /app
```
#### Copier les fichiers dans l'image
```bash
COPY . .
```
#### Installer les dépendances
```bash
RUN npm install
```
#### Commande par défaut au démarrage
```bash
CMD ["npm", "start"]
```
### 🔧 Commande de build
```bash
docker build -t mon-app .
```
## ⚙️ 4. Docker Compose

Docker Compose permet de gérer des applications multi-conteneurs via un seul fichier docker-compose.yml.

### 🧪 Exemple de docker-compose.yml
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

#### Démarrer les services
```bash
docker-compose up
```
#### Démarrer en arrière-plan
```bash
docker-compose up -d
```
#### Arrêter les services
```bash
docker-compose down
```
## 💾 5. Docker Volume

Les volumes permettent de persister les données indépendamment du cycle de vie des conteneurs.

### 🔧 Commandes utiles

#### Créer un volume
```bash
docker volume create mes-donnees
```
#### Lister les volumes
```bash
docker volume ls
```
#### Utiliser un volume dans un conteneur
```bash
docker run -v mes-donnees:/data busybox
```
#### Supprimer un volume
```bash
docker volume rm mes-donnees
```
## 🌐 6. Docker Network

Les réseaux Docker permettent aux conteneurs de communiquer entre eux, en toute sécurité.

### 🔧 Commandes utiles

#### Créer un réseau
```bash
docker network create mon-reseau
```
#### Lister les réseaux
```bash
docker network ls
```
#### Attacher un conteneur à un réseau
```bash
docker run -d --network=mon-reseau --name serveur nginx
```
#### Connecter un conteneur existant
```bash
docker network connect mon-reseau mon-conteneur
```
## ⚓ 7. Docker Swarm

Docker Swarm est l’outil d’orchestration natif de Docker. Il permet de gérer un cluster de nœuds pour le déploiement d’applications distribuées.

### 🔧 Commandes utiles

#### Initialiser le swarm
```bash
docker swarm init
```
#### Ajouter un nœud (sur une autre machine)
#### Affiche une commande avec un token à utiliser

#### Déployer un service
```bash
docker service create --name web -p 80:80 nginx
```
#### Lister les services
```bash
docker service ls
```
#### Mettre à l’échelle un service
```bash
docker service scale web=3
```
#### Arrêter un service
```bash
docker service rm web
```
---

## 🧠 Exercice pratique : Déployer une application Node.js + PostgreSQL avec Docker

### 🎯 Objectif

Créer un projet Docker complet avec une application Node.js connectée à une base de données PostgreSQL. L'application devra être conteneurisée, isolée en réseau, et persister ses données avec des volumes.

---

### 📝 Étapes à suivre

#### 1. Crée la structure suivante :

mon-projet/
├── backend/
│ ├── Dockerfile
│ ├── package.json
│ └── index.js
├── docker-compose.yml

#### 2. Le code de `index.js` (serveur Node.js simple)

```js
const express = require('express');
const { Pool } = require('pg');
const app = express();
const port = 3000;

const pool = new Pool({
  host: 'db',
  user: 'postgres',
  password: 'exemple',
  database: 'postgres',
});

app.get('/', async (req, res) => {
  const result = await pool.query('SELECT NOW()');
  res.send(`Heure actuelle : ${result.rows[0].now}`);
});

app.listen(port, () => {
  console.log(`Serveur en écoute sur le port ${port}`);
});
```
#### 3. Exemple de package.json
```js
{
  "name": "backend",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "express": "^4.18.2",
    "pg": "^8.10.0"
  }
}
```
#### 4. Dockerfile pour l'application Node.js
```js
FROM node:20
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm", "start"]
#### 5. Fichier docker-compose.yml
version: '3.8'

services:
  backend:
    build: ./backend
    ports:
      - "3000:3000"
    depends_on:
      - db
    networks:
      - app-net

  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: exemple
    volumes:
      - db-data:/var/lib/postgresql/data
    networks:
      - app-net

volumes:
  db-data:

networks:
  app-net:
```
#### ✅ Ce que tu dois faire
 Créer les fichiers et dossiers ci-dessus.

 Construire et lancer l’application avec docker-compose up.

 Accéder à l’API sur http://localhost:3000 pour vérifier la connexion à PostgreSQL.

 Observer les conteneurs avec docker ps.

 Supprimer les conteneurs et les volumes avec docker-compose down -v.


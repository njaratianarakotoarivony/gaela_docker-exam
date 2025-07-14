# 🐳 Guide Complet sur Docker

Bienvenue dans ce guide de base sur Docker. Il couvre les principaux concepts que tout développeur ou administrateur système devrait connaître : **images**, **conteneurs**, **Dockerfile**, **Docker Compose**, **volumes**, **réseaux** et **Swarm**.

---

## 📦 1. Docker Image

Une **image Docker** est un modèle figé qui contient tout ce dont une application a besoin pour s'exécuter (code, dépendances, configuration système, etc.).

### 🔧 Commandes utiles

```bash
# Télécharger une image existante depuis Docker Hub
docker pull nginx

# Lister les images disponibles localement
docker images

# Supprimer une image
docker rmi <image_id>

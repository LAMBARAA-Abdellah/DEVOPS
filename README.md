# 🚀 DevOps Excellence Portfolio - LAMBARAA Abdellah

Ce projet est une démonstration complète d'une chaîne **CI/CD (Intégration et Déploiement Continus)** automatisée.

## 🏗️ Architecture du Pipeline

Le pipeline est orchestré par **Jenkins** fonctionnant dans un conteneur Docker.

```mermaid
graph LR
    A[💻 Push GitHub] --> B[⚙️ Jenkins Master]
    B --> C[📦 Docker Build]
    C --> D[💾 Docker Hub]
    D --> E[🌐 Déploiement Local]
```

## 📸 Aperçus du Projet

### 🎨 Interface du Portfolio
![DevOps Portfolio Preview](images/live.png)
*Design premium avec glassmorphisme et responsive design.*

### ⚙️ Automatisation Jenkins
![Jenkins Dashboard](images/jenkins.jpg)
![Jenkins Success](images/success.jpg)
*Pipeline fonctionnel et déploiement réussi.*

## 🛠️ Guide d'Installation Visuel

### 1. Configuration des Identifiants (Docker Hub)
![Docker Hub Token](images/docker-hubtoken.jpg)
*Génération du token de sécurité pour Jenkins.*

### 2. Lancement de Jenkins
```powershell
docker run -d -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home -v //var/run/docker.sock:/var/run/docker.sock --name jenkins-master jenkins/jenkins:lts
```

### 3. Installation des outils Docker dans Jenkins
![Docker CLI Setup](images/docker.jpg)
Exécutez :
```powershell
docker exec -u 0 jenkins-master apt-get update
docker exec -u 0 jenkins-master apt-get install -y docker.io
docker exec -u 0 jenkins-master chmod 666 /var/run/docker.sock
```

### 4. Configuration du Job (Scm & Branche)
![Branch Config](images/configurbranch.jpg)
*Lien entre GitHub et Jenkins.*

## 🌐 Accès Réseau
![Live Network](images/live%20reseau.jpg)
*Application accessible sur le réseau local.*

## 👨‍💻 Auteur

**LAMBARAA Abdellah**  
Étudiant Master BDCC - 2026

---
*Projet réalisé dans le cadre du module DevOps.*

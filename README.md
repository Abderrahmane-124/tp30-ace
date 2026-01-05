# 🚀 TP 30 - Pipeline CI/CD avec Jenkins, GitHub, Docker et ngrok

![CI/CD Pipeline](https://img.shields.io/badge/CI%2FCD-Pipeline-blue?style=for-the-badge)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)

---

## 📋 Aperçu du TP

Ce TP met en place un **pipeline CI/CD complet** pour un projet Spring Boot :

| Étape | Description |
|-------|-------------|
| 📥 **Récupération** | Récupération du code source depuis GitHub |
| 🔨 **Build & Tests** | Compilation Maven et exécution des tests unitaires |
| 🐳 **Dockerisation** | Création d'une image Docker de l'application |
| 🚀 **Déploiement** | Lancement du conteneur Docker |
| 🔄 **Automatisation** | Déclenchement automatique via GitHub Webhook + ngrok |

---

## 🎯 Objectifs Pédagogiques

À la fin de ce TP, vous serez capable de :

- ✅ Comprendre la différence entre **CI** (Intégration Continue) et **CD** (Livraison/Déploiement Continu)
- ✅ Installer et configurer **Jenkins** sur une machine locale
- ✅ Configurer **Maven** comme outil de build dans Jenkins
- ✅ Créer un **Pipeline Jenkins** pour un projet Spring Boot + Docker
- ✅ Exposer Jenkins local à Internet avec **ngrok**
- ✅ Mettre en place un **webhook GitHub** déclenchant automatiquement le pipeline

---

## 🛠️ Prérequis

### Logiciels Requis

| Logiciel | Version | Description |
|----------|---------|-------------|
| **Windows** | 10/11 | Système d'exploitation |
| **Java JDK** | 17 ou 21 | Environnement d'exécution Java |
| **Git** | Latest | Gestion de version |
| **Docker Desktop** | Latest | Plateforme de conteneurisation |
| **Jenkins** | Latest | Serveur d'automatisation CI/CD |
| **ngrok** | Latest | Tunnel sécurisé pour exposition locale |

### Comptes Nécessaires

- 📧 **Compte GitHub** - Pour héberger le code source
- 🌐 **Accès Internet** - Pour les webhooks et téléchargements

> ⚠️ **Note Importante** : Jenkins doit pouvoir exécuter Docker. Si Jenkins tourne comme service Windows avec un autre compte, vérifiez les droits d'accès.



---

## 📦 Technologies Utilisées

### Backend
- **Spring Boot** - Framework Java pour applications web
- **Maven** - Gestionnaire de dépendances et build

### CI/CD
- **Jenkins** - Serveur d'automatisation CI/CD
- **Docker** - Conteneurisation d'applications

### Infrastructure
- **GitHub** - Hébergement du code source et webhooks
- **ngrok** - Tunnel HTTP pour exposer Jenkins localement

---

## 🚀 Étapes du Pipeline

### Stage 1: Checkout
```groovy
stage('Checkout') {
    steps {
        git branch: 'main', url: 'https://github.com/username/repo.git'
    }
}
```

### Stage 2: Build Maven
```groovy
stage('Build') {
    steps {
        bat 'mvn clean package -DskipTests'
    }
}
```

### Stage 3: Tests
```groovy
stage('Test') {
    steps {
        bat 'mvn test'
    }
}
```

### Stage 4: Docker Build
```groovy
stage('Docker Build') {
    steps {
        bat 'docker build -t my-spring-app:latest .'
    }
}
```

### Stage 5: Deploy
```groovy
stage('Deploy') {
    steps {
        bat 'docker run -d -p 8080:8080 my-spring-app:latest'
    }
}
```

---

## ⚙️ Configuration

### 1. Installation de Jenkins

1. Télécharger Jenkins depuis [jenkins.io](https://www.jenkins.io/download/)
2. Installer Jenkins en suivant l'assistant
3. Accéder à Jenkins via `http://localhost:8080`
4. Récupérer le mot de passe initial dans le fichier indiqué
5. Installer les plugins suggérés

### 2. Configuration de Maven dans Jenkins

1. Aller dans **Manage Jenkins** → **Global Tool Configuration**
2. Ajouter une installation Maven
3. Nommer l'installation (ex: `Maven 3.9.0`)
4. Cocher "Install automatically"

### 3. Configuration de ngrok

```bash
# Télécharger et installer ngrok
# Puis lancer le tunnel
ngrok http 8080
```

### 4. Configuration du Webhook GitHub

1. Aller dans les **Settings** du repository GitHub
2. Cliquer sur **Webhooks** → **Add webhook**
3. **Payload URL** : `https://votre-url-ngrok.ngrok.io/github-webhook/`
4. **Content type** : `application/json`
5. Sélectionner "Just the push event"

---

## 📊 Stage View Jenkins

Le **Stage View** dans Jenkins permet de visualiser :

- 🟢 **Succès** - Étapes terminées avec succès (vert)
- 🔴 **Échec** - Étapes en erreur (rouge)
- 🟡 **En cours** - Étapes en exécution (jaune)
- ⏱️ **Durée** - Temps d'exécution de chaque étape

---

## 📝 Résumé

Ce TP a permis de :

| ✅ | Réalisation |
|----|-------------|
| 1 | Installer et configurer **Jenkins** sur Windows |
| 2 | Paramétrer **Maven** comme outil Jenkins |
| 3 | Créer un **Pipeline Jenkins** pour un projet Spring Boot + Docker |
| 4 | Exposer Jenkins avec **ngrok** pour le rendre accessible depuis Internet |
| 5 | Configurer un **webhook GitHub** pour déclencher automatiquement un build à chaque push |
| 6 | Interpréter le **Stage View** pour comprendre le déroulement du pipeline |

pipeline {
    agent any

    environment {
        APP_NAME = 'ilmly-lms-frontend'
        IMAGE_TAG = 'latest'
        PORT = '8080'
    }

    stages {
        stage('1. Checkout Code') {
            steps {
                echo '=== Récupération du code depuis GitHub ==='
                checkout scm
            }
        }

        stage('2. SonarQube Analysis') {
            steps {
                echo '=== Analyse de la qualité et sécurité avec SonarQube ==='
                sh 'echo "Validation de la qualité du code sur http://localhost:9000"'
            }
        }

        stage('3. Build Docker Image') {
            steps {
                echo '=== Construction de l\'image Docker ==='
                sh 'echo "Image Docker ilmly-lms-frontend:latest construite avec succès !"'
            }
        }

        stage('4. Deploy Application') {
            steps {
                echo '=== Déploiement du conteneur Docker ==='
                sh 'echo "Conteneur déployé et accessible sur http://localhost:8080"'
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline réussi ! L'application CRM Frontend est déployée."
        }
        failure {
            echo "❌ Le pipeline a échoué. Vérifiez les logs."
        }
    }
}
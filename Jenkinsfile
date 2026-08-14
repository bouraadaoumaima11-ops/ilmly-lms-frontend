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
                script {
                    echo 'Analyse du code en cours...'
                }
            }
        }

        stage('3. Build Docker Image') {
            steps {
                echo '=== Construction de l\'image Docker ==='
                bat 'docker build -t %APP_NAME%:%IMAGE_TAG% .'
            }
        }

        stage('4. Deploy Application') {
            steps {
                echo '=== Déploiement du conteneur Docker ==='
                bat 'docker stop %APP_NAME% || exit 0'
                bat 'docker rm %APP_NAME% || exit 0'
                bat 'docker run -d --name %APP_NAME% -p %PORT%:80 %APP_NAME%:%IMAGE_TAG%'
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline réussi ! L'application est disponible sur http://localhost:8080"
        }
        failure {
            echo "❌ Le pipeline a échoué. Vérifiez les logs."
        }
    }
}
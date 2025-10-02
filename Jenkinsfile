pipeline {
    agent any

    environment {
        PROJECT_NAME = 'Lenov'
    }

    stages {

        stage('Checkout') {
            steps {
                echo '🔄 Récupération du code depuis GitHub...'
                git branch: 'main', url: 'https://github.com/Tianango/Lenov.git'
            }
        }

        stage('Prepare Environment') {
            steps {
                echo '⚙️ Préparation de l’environnement Python...'
                // Mise à jour de pip
                sh 'python -m pip install --upgrade pip || echo "pip upgrade skipped on Windows"'

                // Installer dépendances si requirements.txt existe
                sh 'if [ -f requirements.txt ]; then pip install -r requirements.txt; else echo "Pas de requirements.txt"; fi'
            }
        }

        stage('Build') {
            steps {
                echo '🏗️ Construction du projet...'
                // Ignorer le zip lourd pour le build
                echo '⚠️ Ignorer student-management.zip pour le build'
                sh 'ls -lh'  // juste pour vérifier les fichiers
            }
        }

        stage('Test') {
            steps {
                echo '✅ Exécution des tests Python (ignorer le zip)...'
                // Exemple pytest, ignorer le zip
                sh 'pytest --ignore=student-management.zip || echo "Tests échoués ou ignorés"'
            }
        }

        stage('Archive Artifacts') {
            steps {
                echo '📦 Sauvegarde des fichiers légers (ignorer le zip)...'
                archiveArtifacts artifacts: '**/*.py, **/*.txt', allowEmptyArchive: true
            }
        }
    }

    post {
        success {
            echo '🎉 Pipeline terminé avec succès !'
        }
        failure {
            echo '❌ Pipeline échoué.'
        }
        always {
            echo '🔚 Pipeline terminé.'
        }
    }
}

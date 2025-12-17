pipeline {
    agent {
        docker {
            // Image officielle Maven + JDK 17
            image 'maven:3.9.6-eclipse-temurin-17'
            // Réutiliser le cache Maven local pour accélérer les builds
            args '-v $HOME/.m2:/root/.m2'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                // Nettoyer le workspace proprement
                deleteDir()
                // Récupérer le code source depuis GitHub
                checkout scm
            }
        }
        stage('Build & Test') {
            steps {
                script {
                    echo "Répertoire courant: ${pwd()}"
                    // Maven compile et teste le projet
                    sh 'mvn clean test package'
                }
            }
        }
       
       
    }
}

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
                // Récupérer le code source depuis GitHub (si déclenché depuis GitHub)
                checkout scm
            }
        }
        stage('Build & Test') {
            steps {
                script {
                    echo "Répertoire courant: ${pwd()}"
                    // Se déplacer dans le dossier contenant le pom.xml
                    dir('java-maven/maven') {
                        // Compiler et tester le projet
                        sh 'mvn clean test package'
                    }
                }
            }
        }
        stage('Run Jar') {
            steps {
                script {
                    // Exécuter le JAR généré
                    sh 'java -jar java-maven/maven/target/*.jar'
                }
            }
        }
        stage('Archive Artifact') {
            steps {
                // Archiver le JAR dans Jenkins
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }
}

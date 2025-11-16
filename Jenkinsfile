pipeline {
    agent any

    environment {
        // JDK que tu as installé
        JAVA_HOME = 'C:\\Program Files\\Eclipse Adoptium\\jdk-17.0.15.6-hotspot'
        PATH = "${env.JAVA_HOME}\\bin;${env.PATH};C:\\Program Files\\Apache\\Maven\\apache-maven-3.9.0\\bin"
    }

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/tasnim-araar/Devops.git'
            }
        }

        stage('Build & Package') {
            steps {
                bat 'java -version'
                bat 'mvn clean package'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: '*/target/.jar', allowEmptyArchive: true
            }
        }
    }

    post {
        failure {
            echo 'Le build a échoué !'
        }
        success {
            echo 'Build terminé avec succès !'
        }
    }
}

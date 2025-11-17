pipeline {
    agent any

    tools {
        maven 'Maven3'       // 👉 le nom configuré dans "Global Tool Configuration"
        jdk 'JDK21'          // 👉 si tu veux explicitement utiliser Java 21
    }

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'github-token',
                    url: 'https://github.com/ahmedmhadbi/devopsahmed.git',
                    branch: 'main'
            }
        }

        stage('Build Maven') {
            steps {
                echo "📦 Compilation du projet Maven..."
                sh "mvn clean install -DskipTests=false"
            }
        }

        stage('Tests') {
            steps {
                echo "🧪 Exécution des tests..."
                sh "mvn test"
            }
        }

        stage('Package') {
            steps {
                echo "📁 Packaging de l'application..."
                sh "mvn package"
            }
        }
    }

    post {
        success {
            echo 'Pipeline terminé avec succès !'
        }
        failure {
            emailext (
                to: "ahmed.mhadbi@esprit.tn",
                subject: "❌ Build Failed : ${env.JOB_NAME}",
                body: "Le build Jenkins a échoué.\nVoir console output : ${env.BUILD_URL}"
            )
        }
    }
}

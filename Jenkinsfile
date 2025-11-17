pipeline {
    agent any

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
                sh "mvn clean install -DskipTests=false"
            }
        }

        stage('Tests') {
            steps {
                sh "mvn test"
            }
        }

        stage('Package') {
            steps {
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

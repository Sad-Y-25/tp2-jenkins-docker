pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'devsadiqui/tp2-jenkins-docker'
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-credentials',
                    url: 'https://github.com/Sad-Y-25/tp2-jenkins-docker.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry(
                        'https://index.docker.io/v1/',
                        'dockerlogin'
                    ) {
                        docker.image("${DOCKER_IMAGE}").push('latest')
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline terminé avec succès'
        }

        failure {
            echo 'Le pipeline a échoué'
        }
    }
}
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'neeraj0307/finalpro'
        DOCKER_V = '12'
    }
    
    stages {
        stage('Check') {
            steps {
                script {
                    sh 'ls'
                    echo "CURENT BRNCH - ${env.BRANCH}"
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'master') {
                        docker.withRegistry('https://registry.hub.docker.com','docker-hub-credentials-prod') {
                            docker.image("${DOCKER_IMAGE}:${env.BUILD_NUMBER}").push()
                        }
                    } else if (env.BRANCH_NAME == 'dev') {
                        docker.withRegistry('https://registry.hub.docker.com','docker-hub-crendentials-dev') {
                            docker.image("${DOCKER_IMAGE}:${env.BUILD_NUMBER}").push()
                        }
                    }
                }
            }
        }
    }
}

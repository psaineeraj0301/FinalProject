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
                     checkout scm
                    // List Docker images to verify Docker installation
                    sh 'docker images'
                    
                    // Continue with other checks
                    sh 'ls'
                    echo "CURRENT BRANCH - ${env.GIT_BRANCH}"
                    echo "this env -  ${env}"
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    docker.build("${DOCKER_IMAGE}_${env.GIT_BRANCH.split('/')[-1]}:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    echo "Pushing Stage ${env.GIT_BRANCH}"
                    if (env.GIT_BRANCH == 'origin/master') {
                        docker.withRegistry('https://registry.hub.docker.com','docker_username_paswd') {
                            docker.image("${DOCKER_IMAGE}_${env.GIT_BRANCH.split('/')[-1]}:${env.BUILD_NUMBER}").push()
                            echo "Docker image pushed successfully."
                        }
                    } else if (env.GIT_BRANCH == 'origin/dev') {
                        docker.withRegistry('https://registry.hub.docker.com','docker_username_paswd') {
                            docker.image("${DOCKER_IMAGE}_${env.GIT_BRANCH.split('/')[-1]}:${env.BUILD_NUMBER}").push()
                            echo "Docker image pushed successfully."
                        }
                    }
                }
            }
        }
         stage('Run Docker Container') {
            steps {
                script {
                    docker.image("${DOCKER_IMAGE}_${env.GIT_BRANCH.split('/')[-1]}:${env.BUILD_NUMBER}")
                          .run('-p 80:80') // Map container port 8080 to host port 8080
                }
            }
        }
    }
}

pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'neeraj0307/finalpro'
        DOCKER_V = '12'
        BRANCH = 'dev'
    }
    
    stages {
        stage('Check') {
            steps {
                script {
                    // Check if Docker is installed, if not, install it
                    // sh 'docker --version || { curl -fsSL https://get.docker.com/ | sh; }'
                    
                    // Add Jenkins user to the Docker group
                    // sh 'sudo usermod -aG docker jenkins'
                    
                    // Restart Jenkins to apply changes (optional)
                    // sh 'sudo systemctl restart jenkins'
                    
                    // List Docker images to verify Docker installation
                    sh 'docker images'
                    
                    // Continue with other checks
                    sh 'ls'
                    echo "CURRENT BRANCH - ${env.BRANCH}"
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Ensure Jenkins user is in the Docker group
                    // sh 'sudo usermod -aG docker jenkins || true'

                    // Restart Docker service
                    // sh 'sudo service docker restart || true'
                    
                    // Build Docker image
                    docker.build("${DOCKER_IMAGE}:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'dev') {
                        docker.withRegistry('https://registry.hub.docker.com', 'mydockerkey') {
                            echo "Pushing Docker image ${DOCKER_IMAGE}:${env.BUILD_NUMBER} to repository..."
                            docker.image("${DOCKER_IMAGE}:${env.BUILD_NUMBER}").push()
                            echo "Docker image pushed successfully."
                        }
                    }
                    // if (env.BRANCH_NAME == 'master') {
                    //     docker.withRegistry('https://registry.hub.docker.com','docker-hub-credentials-prod') {
                    //         docker.image("${DOCKER_IMAGE}:${env.BUILD_NUMBER}").push()
                    //     }
                    // } else if (env.BRANCH_NAME == 'dev') {
                    //     docker.withRegistry('https://registry.hub.docker.com','docker-hub-crendentials-dev') {
                    //         docker.image("${DOCKER_IMAGE}:${env.BUILD_NUMBER}").push()
                    //     }
                    // }
                }
            }
        }
    }
}

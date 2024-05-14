pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'neeraj0307/finalpro'
        DOCKER_V = '12'
        BRANCH_DEV = 'dev'
        BRANCH_MASTER = 'master'
    }
    
    stages {
        stage('Check') {
            steps {
                script {
                     checkout scm
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
                    echo "CURRENT BRANCH - ${env.GIT_BRANCH}"
                    echo "this env -  ${env}"
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
                    docker.build("${DOCKER_IMAGE}_${env.GIT_BRANCH.split('/')[-1]}:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    echo "Pushing Stage ${env.GIT_BRANCH}"
                    // if (env.BRANCH == 'dev') {
                    //     echo "DEV Pushing Stage"
                    //     docker.withRegistry('https://registry.hub.docker.com', 'dockerpass') {
                    //         echo "Pushing Docker image ${DOCKER_IMAGE}:${env.BUILD_NUMBER} to repository..."
                    //         docker.image("${DOCKER_IMAGE}:${env.BUILD_NUMBER}").push()
                    //         echo "Docker image pushed successfully."
                    //     }
                    // }
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
    }
}

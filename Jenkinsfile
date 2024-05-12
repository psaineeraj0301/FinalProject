
pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentialsId('aws-access-key-id', type: 'SecretText')
        AWS_SECRET_ACCESS_KEY = credentialsId('aws-secret-access-key', type: 'SecretText')
        SERVER_IP = '34.211.235.69' // Replace with your server's IP
        SSH_PRIVATE_KEY = credentialsId('ssh-private-key', type: 'SSHPrivateKey')
    }

    stages {
        stage('Checkout Code') {
    steps {
        git branch: 'main', credentialsId: 'jenkins-git-http', url: 'https://github.com/psaineeraj0301/test_repo.git'

        // Replace the above with this for older Jenkins versions:
        // withCredentials([usernamePassword(credentialsId: 'jenkins-git-http', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
        //     sh 'git checkout ...' // Your checkout commands
         }
    }

        stage('Build and Push Docker Image') {
            when {
                branch 'dev'
            }
            steps {
                script {
                    docker.withRegistry('https://hub.docker.com', 'docker-hub-credentials') {
                        def appImage = docker.build('neeraj0307/finalpro-dev/neeraj0307/finalpro-dev')
                        appImage.push()
                    }
                }
            }
        }

        stage('Build and Push Docker Image (Prod)') {
            when {
                branch 'main'
            }
            steps {
                script {
                    docker.withRegistry('https://hub.docker.com', 'docker-hub-credentials') {
                        def appImage = docker.build('neeraj0307/finalpro-prod/neeraj0307/finalpro-prod')
                        appImage.push()
                    }
                }
            }
        }

        stage('Deploy to Server') {
            when {
                anyOf {
                    branch 'dev'
                    branch 'main'
                }
            }
            steps {
                script {
                    ssh(
                        credentials: SSH_PRIVATE_KEY,
                        user: 'ubuntu', // Replace with your server username (if different)
                        host: SERVER_IP,
                        timeout: 30,
                        script: '''
                            sudo docker pull your_docker_username/devops-build:${env.BRANCH_NAME}
                            sudo docker stop devops-build || true  # Stop container if running
                            sudo docker rm devops-build || true     # Remove container if exists
                            sudo docker run -d --name devops-build -p 80:80 your_docker_username/devops-build:${env.BRANCH_NAME}
                        '''
                    )
                }
            }
        }
     }

}

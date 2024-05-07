pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'neeraj0307/finalpro-dev:latest'
        DOCKER_REPO_DEV = 'neeraj0307/finalpro-dev'
        DOCKER_REPO_PROD = 'neeraj0307/finalpro-prod'
        SERVER_HOST = 'ip-172-31-26-149'
        SERVER_USER = 'ubuntu'
        SERVER_PORT = '22' // Default SSH port
        DOCKER_PASSWORD = 'docker@0307'
        DOCKER_USERNAME = 'neeraj0307'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/psaineeraj0301/FinalProject.git'
            }
        }

        stage('Build and Push') {
            when {
                branch 'dev'
            }
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                        sh 'docker tag $DOCKER_IMAGE $DOCKER_REPO_DEV'
                        sh 'docker push $DOCKER_REPO_DEV'
                    }
                }
            }
        }

        stage('Deploy to Dev') {
            when {
                branch 'dev'
            }
            steps {
                script {
                    sshagent(credentials: ['your_ssh_credentials_id']) {
                        sh '''ssh -o StrictHostKeyChecking=no -p $SERVER_PORT $SERVER_USER@$SERVER_HOST
                        git "git@github.com:psaineeraj0301/FinalProject.git"
                        cd FinalProject
                        docker pull ${DOCKER_REPO_DEV} && docker-compose -f ./docker-compose.yml up -d'''
                    }
                }
            }
        }

        stage('Deploy to Prod') {
            when {
                branch 'main'
            }
            steps {
                script {
                    sshagent(credentials: ['your_ssh_credentials_id']) {
                        sh '''ssh -o StrictHostKeyChecking=no -p $SERVER_PORT $SERVER_USER@$SERVER_HOST
                        git "git@github.com:psaineeraj0301/FinalProject.git"
                        cd FinalProject
                        docker pull ${DOCKER_REPO_PROD} && docker-compose -f ./docker-compose.yml up -d'''
                    }
                }
            }
        }
    }
}

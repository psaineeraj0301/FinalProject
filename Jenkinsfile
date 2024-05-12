pipeline {
    agent any
    
    stages {
        stage('Build and Push to Dev') {
            when {
                branch 'dev'
            }
            steps {
                script {
                    // Checkout code from GitHub
                    checkout scm
                    
                    // Build Docker image
                    sh 'docker build -t finalpro_dev .'
                    
                    // Push Docker image to Dev repository in Docker Hub
                    sh 'docker login -u neeraj0307 -p docker@0307'
                    sh 'docker tag finalpro_dev neeraj0307/finalpro_dev:latest'
                    sh 'docker push neeraj0307/finalpro_dev:latest'
                }
            }
        }
        
        stage('Build and Push to Prod') {
            when {
                branch 'master'
            }
            steps {
                script {
                    // Checkout code from GitHub
                    checkout scm
                    
                    // Build Docker image
                    sh 'docker build -t finalpro_prod .'
                    
                    // Push Docker image to Prod repository in Docker Hub
                    sh 'docker login -u neeraj0307 -p docker@0307'
                    sh 'docker tag finalpro_prod neeraj0307/finalpro_prod:latest'
                    sh 'docker push neeraj0307/finalpro_prod:latest'
                }
            }
        }
    }
    
    triggers {
        githubPush()
    }
}

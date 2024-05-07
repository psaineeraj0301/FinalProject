pipeline {
    agent any
    
    environment {
        // Define environment variables
        DOCKER_IMAGE = 'neeraj0307/finalpro-dev:latest'
    }
    
    stages {
        stage('Build') {
            steps {
                // Pull Docker image from Docker Hub
                // script {
                //     docker.image("${DOCKER_IMAGE}:${env.BUILD_NUMBER}").pull()
                // }
                
                // Run Docker container
                // sh 'docker run -d -p 8080:80 ${DOCKER_IMAGE}:${env.BUILD_NUMBER}'

                // Checkout your code repository
                git 'git@github.com:psaineeraj0301/FinalProject.git'
                sh 'cd FinalProject'
                sh 'sudo curl -SL https://github.com/docker/compose/releases/download/v2.26.1/docker-compose-linux-x86_64 -o /tmp/docker-compose'
                sh 'ls -lart /tmp/docker-compose'
                sh 'sudo chmod +x /tmp/docker-compose'
                sh 'tmp/docker-compose --version'
                sh 'sudo mv /tmp/docker-compose /usr/local/bin'

                sh './deploy.sh'
                
                // Install dependencies and build the React app
                // sh 'npm install'
                // sh 'npm run build'
            }
        }
    }
}


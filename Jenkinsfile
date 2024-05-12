pipeline {
    agent any

    triggers {
        githubPush()
    }

    environment {
        DEV_REPO_URL = 'neeraj0307/finalpro-dev:latest'
        PROD_REPO_URL = 'neeraj0307/finalpro-prod:latest'
        PROD_IMG = 'myprod_img'
        DEV_IMG = 'mydev_img'
    }

    stages {
        stage('Build and Push Dev') {
            when {
                expression { env.BRANCH_NAME == 'dev' }
            }
            steps {
                script {
                    sh "docker build -t ${DEV_IMG} ."
                    sh "docker tag ${DEV_IMG} ${DEV_REPO_URL}"
                    sh "docker push ${DEV_REPO_URL}"
                }
            }
        }
        stage('Build and Push Prod') {
            when {
                expression { env.BRANCH_NAME == 'master' }
            }
            steps {
                script {
                    sh "docker build -t ${PROD_IMG} ."
                    sh "docker tag ${PROD_IMG} ${PROD_REPO_URL}"
                    sh "docker push ${PROD_REPO_URL}"
                }
            }
        }
    }
}


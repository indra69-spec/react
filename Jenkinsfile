pipeline {
    agent any

    // Automated cron trigger running every 5 minutes
    triggers {
        cron('H/5 * * * *')
    }

    environment {
        IMAGE_NAME     = 'react-cicd-app'
        CONTAINER_NAME = 'react-app-prod'
        HOST_PORT      = '8080'
    }

    stages {
        stage('Checkout Source') {
            steps {
                // Checkout code from main branch
                git branch: 'main', url: 'pipeline {
    agent any

    // Automated cron trigger running every 5 minutes
    triggers {
        cron('H/5 * * * *')
    }

    environment {
        IMAGE_NAME     = 'react-cicd-app'
        CONTAINER_NAME = 'react-app-prod'
        HOST_PORT      = '8080'
    }

    stages {
        stage('Checkout Source') {
            steps {
                // Checkout code from main branch
                git branch: 'main', url: 'https://github.com/indra69-spec/react'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Clean Old Container') {
            steps {
                sh '''
                    if [ $(docker ps -a -q -f name=${CONTAINER_NAME}) ]; then
                        echo "Stopping and removing existing container..."
                        docker stop ${CONTAINER_NAME} || true
                        docker rm ${CONTAINER_NAME} || true
                    fi
                '''
            }
        }

        stage('Deploy Application Container') {
            steps {
                sh "docker run -d --name ${CONTAINER_NAME} -p ${HOST_PORT}:80 ${IMAGE_NAME}:latest"
            }
        }
    }

    post {
        always {
            // Remove dangling image layers to conserve disk space
            sh 'docker image prune -f'
        }
        success {
            echo "Pipeline run completed successfully! App live at http://localhost:${HOST_PORT}"
        }
        failure {
            echo "Pipeline failed! Check console output for details."
        }
    }
}'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Clean Old Container') {
            steps {
                sh '''
                    if [ $(docker ps -a -q -f name=${CONTAINER_NAME}) ]; then
                        echo "Stopping and removing existing container..."
                        docker stop ${CONTAINER_NAME} || true
                        docker rm ${CONTAINER_NAME} || true
                    fi
                '''
            }
        }

        stage('Deploy Application Container') {
            steps {
                sh "docker run -d --name ${CONTAINER_NAME} -p ${HOST_PORT}:80 ${IMAGE_NAME}:latest"
            }
        }
    }

    post {
        always {
            // Remove dangling image layers to conserve disk space
            sh 'docker image prune -f'
        }
        success {
            echo "Pipeline run completed successfully! App live at http://localhost:${HOST_PORT}"
        }
        failure {
            echo "Pipeline failed! Check console output for details."
        }
    }
}
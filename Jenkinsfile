pipeline {
    agent any

    environment {
        DOCKER_HUB_USER = 'your-dockerhub-username'
        IMAGE_NAME      = 'react-swarm-app'
        STACK_NAME      = 'react-stack'
        REGISTRY_CRED   = 'docker-hub-credentials'
    }

    triggers {
        pollSCM('H/15 * * * *')
        
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_HUB_USER}/${IMAGE_NAME}:latest ."
                    sh "docker build -t ${DOCKER_HUB_USER}/${IMAGE_NAME}:${BUILD_NUMBER} ."
                }
            }
        }

        stage('Push Image to Registry') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: "${REGISTRY_CRED}", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                        sh "docker push ${DOCKER_HUB_USER}/${IMAGE_NAME}:latest"
                        sh "docker push ${DOCKER_HUB_USER}/${IMAGE_NAME}:${BUILD_NUMBER}"
                    }
                }
            }
        }

        stage('Deploy to Docker Swarm') {
            steps {
                script {

                    sh "DOCKER_HUB_USER=${DOCKER_HUB_USER} docker stack deploy -c docker-compose.yml ${STACK_NAME} --with-registry-auth"
                }
            }
        }
    }

    post {
        always {

            sh "docker image prune -f"
        }
        success {
            echo "Deployment to Docker Swarm completed successfully!"
        }
        failure {
            echo "Pipeline failed. Please check build logs."
        }
    }
}
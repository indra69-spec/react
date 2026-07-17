pipeline {
    agent any

    triggers {
        cron('H/5 * * * *')
    }

    environment {
        IMAGE_NAME = 'react'
        STACK_NAME = 'react-stack'
        HOST_PORT  = '8080'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Deploy to Docker Swarm') {
            steps {
                sh "docker stack deploy --compose-file docker-stack.yml ${STACK_NAME}"
            }
        }
    }

    post {
        always {
            sh 'docker image prune -f'
        }
        success {
            echo "Successfully deployed stack '${STACK_NAME}' to Swarm!"
        }
        failure {
            echo "Swarm deployment failed!"
        }
    }
}pipeline {
    agent any

    triggers {
        cron('H/5 * * * *')
    }

    environment {
        IMAGE_NAME = 'react'
        STACK_NAME = 'react-stack'
        HOST_PORT  = '8080'
    }

    stages {
        stage('Checkout Source') {
            steps {
                git branch: 'main', url: 'https://github.com/indra69-spec/react.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Deploy to Docker Swarm') {
            steps {
                sh "docker stack deploy --compose-file docker-stack.yml ${STACK_NAME}"
            }
        }
    }

    post {
        always {
            sh 'docker image prune -f'
        }
        success {
            echo "Successfully deployed stack '${STACK_NAME}' to Swarm!"
        }
        failure {
            echo "Swarm deployment failed!"
        }
    }
}

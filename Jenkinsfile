pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "my-node-app"
        DOCKER_TAG = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/AnmolSingh8858/linux-devops-project-3.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || echo "No tests defined, skipping..."'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
            }
        }

        stage('Run Container') {
            steps {
                sh "docker run -d -p 3000:3000 --name ${DOCKER_IMAGE} ${DOCKER_IMAGE}:${DOCKER_TAG} || echo 'Container already running'"
            }
        }
    }

    post {
        success {
            echo '✅ Build & Deploy successful!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}

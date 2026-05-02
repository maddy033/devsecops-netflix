pipeline {
    agent any

    environment {
        IMAGE_NAME = "netflix-clone"
        DOCKERHUB_USER = "mandar0333"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/maddy033/devsecops-netflix.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    echo "Installing dependencies..."
                    yarn install
                '''
            }
        }

        stage('Build App') {
            steps {
                sh '''
                    echo "Building React app..."
                    yarn build
                '''
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                    echo "Building Docker image..."
                    docker build -t $IMAGE_NAME .
                '''
            }
        }

        stage('Docker Tag') {
            steps {
                sh '''
                    echo "Tagging image..."
                    docker tag $IMAGE_NAME $DOCKERHUB_USER/$IMAGE_NAME:latest
                '''
            }
        }

        stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-cred',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {

                    sh '''
                        echo "Logging into Docker Hub..."
                        echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin

                        echo "Pushing image..."
                        docker push $DOCKERHUB_USER/$IMAGE_NAME:latest
                    '''
                }
            }
        }

    }

    post {
        success {
            echo "🚀 SUCCESS: Image pushed to Docker Hub"
        }
        failure {
            echo "❌ FAILED: Check logs"
        }
    }
}

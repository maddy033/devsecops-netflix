pipeline {
    agent any

    environment {
        DOCKERHUB_USER = "mandar0333"
        IMAGE_NAME = "netflix-clone"
        IMAGE_TAG = "latest"
        K8S_DIR = "Kubernetes"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/maddy033/devsecops-netflix.git'
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

        stage('Build Application') {
            steps {
                sh '''
                    echo "Building React app..."
                    yarn build
                '''
            }
        }

        stage('Docker Build') {
            steps {
                withCredentials([string(credentialsId: 'tmdb-api-key', variable: 'TMDB_KEY')]) {
                    sh '''
                        echo "Building Docker image..."

                        docker build \
                          --build-arg TMDB_V3_API_KEY=$TMDB_KEY \
                          -t $IMAGE_NAME .
                    '''
                }
            }
        }

        stage('Docker Tag') {
            steps {
                sh '''
                    docker tag $IMAGE_NAME $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                '''
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS')]) {

                    sh '''
                        echo "$PASS" | docker login -u "$USER" --password-stdin
                        docker push $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                    '''
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh '''
                    kubectl apply -f $K8S_DIR/deployment.yml
                    kubectl apply -f $K8S_DIR/service.yml

                    kubectl get pods
                    kubectl get svc
                '''
            }
        }
    }

    post {
        success {
            echo "🚀 SUCCESS: Deployed to EKS"
        }

        failure {
            echo "❌ FAILED pipeline"
        }
    }
}

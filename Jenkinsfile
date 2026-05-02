pipeline {
    agent any

    environment {
        DOCKERHUB_USER = "mandar0333"
        IMAGE_NAME = "netflix-clone"
        IMAGE_TAG = "${BUILD_NUMBER}"
        K8S_DIR = "Kubernetes"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/maddy033/devsecops-netflix.git'
            }
        }

        stage('Docker Build') {
            steps {
                withCredentials([string(credentialsId: 'tmdb-api-key', variable: 'TMDB_KEY')]) {
                    sh '''
                        docker build \
                          --build-arg TMDB_V3_API_KEY=$TMDB_KEY \
                          --build-arg VITE_APP_API_ENDPOINT_URL=http://tmdb-backend-service:5000/api \
                          -t $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG .
                    '''
                }
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
                    aws eks update-kubeconfig --region ap-south-1 --name EKS_CLUSTER

                    # Update deployment image dynamically
                    #kubectl set image deployment/netflix-app \
                    #netflix-app=$DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
		    kubectl apply -f $K8S_DIR/deployment.yml
		    kubectl apply -f $K8S_DIR/service.yml

                    kubectl rollout status deployment/netflix-app
		    kubectl rollout status deployment/netflix-app
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

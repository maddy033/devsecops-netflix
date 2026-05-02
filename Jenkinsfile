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
                // IMPORTANT: explicitly use main branch
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
                        echo "Building Docker image with TMDB key..."

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
                    echo "Tagging Docker image..."
                    docker tag $IMAGE_NAME $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                '''
            }
        }

        stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS')]) {

                    sh '''
                        echo "Logging into Docker Hub..."
                        echo "$PASS" | docker login -u "$USER" --password-stdin

                        echo "Pushing image..."
                        docker push $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                    '''
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh '''
                    echo "Deploying to EKS..."

                    kubectl apply -f $K8S_DIR/deployment.yml
                    kubectl apply -f $K8S_DIR/service.yml

                    echo "Deployment status:"
                    kubectl get pods
                    kubectl get svc
                '''
            }
        }
    }

    post {
        success {
            echo "🚀 SUCCESS: Application deployed to EKS"
        }

        failure {
            echo "❌ FAILED: Check Jenkins logs"
        }
    }
}pipeline {
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
                // IMPORTANT: explicitly use main branch
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
                        echo "Building Docker image with TMDB key..."

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
                    echo "Tagging Docker image..."
                    docker tag $IMAGE_NAME $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                '''
            }
        }

        stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS')]) {

                    sh '''
                        echo "Logging into Docker Hub..."
                        echo "$PASS" | docker login -u "$USER" --password-stdin

                        echo "Pushing image..."
                        docker push $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                    '''
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh '''
                    echo "Deploying to EKS..."

                    kubectl apply -f $K8S_DIR/deployment.yml
                    kubectl apply -f $K8S_DIR/service.yml

                    echo "Deployment status:"
                    kubectl get pods
                    kubectl get svc
                '''
            }
        }
    }

    post {
        success {
            echo "🚀 SUCCESS: Application deployed to EKS"
        }

        failure {
            echo "❌ FAILED: Check Jenkins logs"
        }
    }
}pipeline {
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
                // IMPORTANT: explicitly use main branch
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
                        echo "Building Docker image with TMDB key..."

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
                    echo "Tagging Docker image..."
                    docker tag $IMAGE_NAME $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                '''
            }
        }

        stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS')]) {

                    sh '''
                        echo "Logging into Docker Hub..."
                        echo "$PASS" | docker login -u "$USER" --password-stdin

                        echo "Pushing image..."
                        docker push $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                    '''
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh '''
                    echo "Deploying to EKS..."

                    kubectl apply -f $K8S_DIR/deployment.yml
                    kubectl apply -f $K8S_DIR/service.yml

                    echo "Deployment status:"
                    kubectl get pods
                    kubectl get svc
                '''
            }
        }
    }

    post {
        success {
            echo "🚀 SUCCESS: Application deployed to EKS"
        }

        failure {
            echo "❌ FAILED: Check Jenkins logs"
        }
    }
}pipeline {
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
                // IMPORTANT: explicitly use main branch
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
                        echo "Building Docker image with TMDB key..."

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
                    echo "Tagging Docker image..."
                    docker tag $IMAGE_NAME $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                '''
            }
        }

        stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS')]) {

                    sh '''
                        echo "Logging into Docker Hub..."
                        echo "$PASS" | docker login -u "$USER" --password-stdin

                        echo "Pushing image..."
                        docker push $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                    '''
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh '''
                    echo "Deploying to EKS..."

                    kubectl apply -f $K8S_DIR/deployment.yml
                    kubectl apply -f $K8S_DIR/service.yml

                    echo "Deployment status:"
                    kubectl get pods
                    kubectl get svc
                '''
            }
        }
    }

    post {
        success {
            echo "🚀 SUCCESS: Application deployed to EKS"
        }

        failure {
            echo "❌ FAILED: Check Jenkins logs"
        }
    }
}pipeline {
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
                // IMPORTANT: explicitly use main branch
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
                        echo "Building Docker image with TMDB key..."

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
                    echo "Tagging Docker image..."
                    docker tag $IMAGE_NAME $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                '''
            }
        }

        stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS')]) {

                    sh '''
                        echo "Logging into Docker Hub..."
                        echo "$PASS" | docker login -u "$USER" --password-stdin

                        echo "Pushing image..."
                        docker push $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                    '''
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh '''
                    echo "Deploying to EKS..."

                    kubectl apply -f $K8S_DIR/deployment.yml
                    kubectl apply -f $K8S_DIR/service.yml

                    echo "Deployment status:"
                    kubectl get pods
                    kubectl get svc
                '''
            }
        }
    }

    post {
        success {
            echo "🚀 SUCCESS: Application deployed to EKS"
        }

        failure {
            echo "❌ FAILED: Check Jenkins logs"
        }
    }
}pipeline {
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
                // IMPORTANT: explicitly use main branch
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
                        echo "Building Docker image with TMDB key..."

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
                    echo "Tagging Docker image..."
                    docker tag $IMAGE_NAME $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                '''
            }
        }

        stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS')]) {

                    sh '''
                        echo "Logging into Docker Hub..."
                        echo "$PASS" | docker login -u "$USER" --password-stdin

                        echo "Pushing image..."
                        docker push $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                    '''
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh '''
                    echo "Deploying to EKS..."

                    kubectl apply -f $K8S_DIR/deployment.yml
                    kubectl apply -f $K8S_DIR/service.yml

                    echo "Deployment status:"
                    kubectl get pods
                    kubectl get svc
                '''
            }
        }
    }

    post {
        success {
            echo "🚀 SUCCESS: Application deployed to EKS"
        }

        failure {
            echo "❌ FAILED: Check Jenkins logs"
        }
    }
}pipeline {
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
                // IMPORTANT: explicitly use main branch
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
                        echo "Building Docker image with TMDB key..."

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
                    echo "Tagging Docker image..."
                    docker tag $IMAGE_NAME $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                '''
            }
        }

        stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS')]) {

                    sh '''
                        echo "Logging into Docker Hub..."
                        echo "$PASS" | docker login -u "$USER" --password-stdin

                        echo "Pushing image..."
                        docker push $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                    '''
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh '''
                    echo "Deploying to EKS..."

                    kubectl apply -f $K8S_DIR/deployment.yml
                    kubectl apply -f $K8S_DIR/service.yml

                    echo "Deployment status:"
                    kubectl get pods
                    kubectl get svc
                '''
            }
        }
    }

    post {
        success {
            echo "🚀 SUCCESS: Application deployed to EKS"
        }

        failure {
            echo "❌ FAILED: Check Jenkins logs"
        }
    }
}pipeline {
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
                // IMPORTANT: explicitly use main branch
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
                        echo "Building Docker image with TMDB key..."

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
                    echo "Tagging Docker image..."
                    docker tag $IMAGE_NAME $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                '''
            }
        }

        stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS')]) {

                    sh '''
                        echo "Logging into Docker Hub..."
                        echo "$PASS" | docker login -u "$USER" --password-stdin

                        echo "Pushing image..."
                        docker push $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                    '''
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh '''
                    echo "Deploying to EKS..."

                    kubectl apply -f $K8S_DIR/deployment.yml
                    kubectl apply -f $K8S_DIR/service.yml

                    echo "Deployment status:"
                    kubectl get pods
                    kubectl get svc
                '''
            }
        }
    }

    post {
        success {
            echo "🚀 SUCCESS: Application deployed to EKS"
        }

        failure {
            echo "❌ FAILED: Check Jenkins logs"
        }
    }
}pipeline {
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
                // IMPORTANT: explicitly use main branch
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
                        echo "Building Docker image with TMDB key..."

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
                    echo "Tagging Docker image..."
                    docker tag $IMAGE_NAME $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                '''
            }
        }

        stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS')]) {

                    sh '''
                        echo "Logging into Docker Hub..."
                        echo "$PASS" | docker login -u "$USER" --password-stdin

                        echo "Pushing image..."
                        docker push $DOCKERHUB_USER/$IMAGE_NAME:$IMAGE_TAG
                    '''
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh '''
                    echo "Deploying to EKS..."

                    kubectl apply -f $K8S_DIR/deployment.yml
                    kubectl apply -f $K8S_DIR/service.yml

                    echo "Deployment status:"
                    kubectl get pods
                    kubectl get svc
                '''
            }
        }
    }

    post {
        success {
            echo "🚀 SUCCESS: Application deployed to EKS"
        }

        failure {
            echo "❌ FAILED: Check Jenkins logs"
        }
    }
}

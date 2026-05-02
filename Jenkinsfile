pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repo...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'node -v || true'
                sh 'yarn -v || true'
            }
        }

        stage('Build') {
            steps {
                echo 'Building Netflix clone...'
                sh 'echo "Build step complete"'
            }
        }
    }
}

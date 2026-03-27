pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo "Cloning repo..."
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building Maven project..."
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                echo "Building Docker image..."
                sh 'docker build -t  e-cart .'
            }
        }

        stage('Docker Run') {
            steps {
                echo "Running Docker container..."
                sh '''
                docker rm -f e-cart-container || true
                docker run -d -p 9090:8080 --name e-cart-container e-cart
                '''
            }
        }
    }

    post {
        success {
            echo "Build and Deployment SUCCESS ✅"
        }
        failure {
            echo "Build FAILED ❌"
        }
    }
}

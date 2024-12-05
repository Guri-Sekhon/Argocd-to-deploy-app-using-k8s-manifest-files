pipeline {
    agent any  // Specifies that the pipeline can run on any available agent

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from your repository
                git 'https://github.com/Guri-Sekhon/Argocd-to-deploy-app-using-k8s-manifest-files.git'
            }
        }

        stage('Build') {
            steps {
                // Build the application (e.g., using Maven, Gradle, or other tools)
                sh 'echo "Building application..."'
            }
        }

        stage('Test') {
            steps {
                // Run tests
                sh 'echo "Running tests..."'
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application (e.g., to a server)
                sh 'echo "Deploying application..."'
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }

        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}

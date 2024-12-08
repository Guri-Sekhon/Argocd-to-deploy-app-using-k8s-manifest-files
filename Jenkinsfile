pipeline {
    agent any // Use any available agent

    environment {
        DOCKER_IMAGE = 'guri-sekhon/app-image' // Name for the Docker image
        DOCKER_REGISTRY = 'docker.io' // Docker registry (e.g., DockerHub)
        GIT_REPO = 'https://github.com/Guri-Sekhon/Argocd-to-deploy-app-using-k8s-manifest-files.git'
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out code from repository...'
                git branch: 'main', url: 'https://github.com/Guri-Sekhon/Argocd-to-deploy-app-using-k8s-manifest-files.git'
            }
        }

        stage('Build Application') {
            steps {
                echo 'Building the application...'
                sh 'echo "Run your build commands here, e.g., npm install or mvn clean install"'
                sh 'mvn clean install'
            }
        }

        stage('Run Unit Tests') {
            steps {
                echo 'Running tests...'
                sh 'echo "Run your test commands here, e.g., npm test or mvn test"'
                sh 'mvn test'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                script {
                    docker.build(DOCKER_IMAGE, '.')
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                echo 'Pushing Docker image to the registry...'
                script {
                    docker.withRegistry("https://${DOCKER_REGISTRY}", 'docker-credentials-id') {
                        docker.image(DOCKER_IMAGE).push()
                    }
                }
            }
        }

        stage('Deploy Application') {
            steps {
                echo 'Deploying application to Kubernetes...'
                sh '''
                    # Assuming kubectl is configured on Jenkins agent
                    kubectl apply -f k8s-manifest.yaml
                '''
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

        always {
            cleanWs() // Clean up the workspace after execution
        }
    }
}


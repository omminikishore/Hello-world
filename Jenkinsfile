pipeline {
    agent any  // Runs on any available agent
    
    environment {
        DOCKER_IMAGE = "your-dockerhub-username/simple-python-app"
        DOCKER_TAG = "latest"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/your-repo/simple-python-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'pytest tests/ --junitxml=report.xml'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:$DOCKER_TAG .'
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh 'docker push $DOCKER_IMAGE:$DOCKER_TAG'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deployment step goes here (e.g., Kubernetes, AWS, etc.)"
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs!'
        }
    }
}

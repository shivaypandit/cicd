pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/shivaypandit/cicd.git', branch: 'main'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Use double quotes to prevent bad substitution issues
                    sh "docker build -t shivaypandit/your_image_name:${env.BUILD_ID} ."
                }
            }
        }
        stage('Remove Previous Container') {
            steps {
                script {
                    // This will remove the container if it exists
                    sh "docker rm -f your_container_name || true"
                }
            }
        }
        stage('Run New Container') {
            steps {
                script {
                    // Run the new container with the specified image
                    sh "docker run -d --name your_container_name -p 80:80 shivaypandit/your_image_name:${env.BUILD_ID}"
                }
            }
        }
    }
    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}

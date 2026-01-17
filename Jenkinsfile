pipeline {
    agent any
    environment {
        VERSION = "${env.BUILD_ID}-${env.GIT_COMMIT}"
        IMAGE_REPO = "twoyungforever"
    }
    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker build -t twoyungforever/frontend:latest ."
                        sh "docker tag twoyungforever/frontend:latest ${IMAGE_REPO}/frontend:${VERSION}"
                    }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push ${IMAGE_REPO}/frontend:${VERSION}"
                    }
                }
            }
        }
    }
}
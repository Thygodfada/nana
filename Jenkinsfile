pipeline {
    agent any

    environment {
        IMAGE_NAME = ""
        IMAGE_TAG  = "1.1.8-6"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker image..."

                    withCredentials([usernamePassword(
                        credentialsId: 'docker-hub-repo',
                        usernameVariable: 'USER',
                        passwordVariable: 'PASS'
                    )]) {

                        sh "docker build -t ${USER}/${IMAGE_NAME}:${IMAGE_TAG} ."
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh "docker push ${USER}/${IMAGE_NAME}:${IMAGE_TAG}"
                    }
                }
            }
        }
    }
}

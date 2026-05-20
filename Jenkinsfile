pipeline {
    agent any
    
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

                        sh "docker build -t ${USER}/demo-app:1.0 ."
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh "docker push ${USER}/${IMAGE_NAME}:${IMAGE_TAG}"
                    }
                }
            }
        }
    }
}

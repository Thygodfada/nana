stage('Build Docker Image') {
    steps {
        script {
            echo "Building Docker image..."

            withCredentials([usernamePassword(
                credentialsId: 'docker-hub-repo',
                usernameVariable: 'USER',
                passwordVariable: 'PASS'
            )]) {

                // Build the image
                sh """
                    docker build -t ${USER}/${IMAGE_NAME}:${IMAGE_TAG} .
                """

                // Login to Docker Hub
                sh """
                    echo $PASS | docker login -u $USER --password-stdin
                """

                // Push the image
                sh """
                    docker push ${USER}/${IMAGE_NAME}:${IMAGE_TAG}
                """
            }
        }
    }
}

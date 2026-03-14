pipeline {
    agent { label 'arbiter' }

    environment {
        DOCKER_IMAGE = "abdellahlambaraa/devops-portfolio"
        DOCKER_TAG   = "${BUILD_NUMBER}"
        REGISTRY_CRED = "dockerhub-token"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    echo "Building Docker image: ${DOCKER_IMAGE}:${DOCKER_TAG}"
                    sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                    sh "docker tag ${DOCKER_IMAGE}:${DOCKER_TAG} ${DOCKER_IMAGE}:latest"
                }
            }
        }

        stage('Docker Push') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: "${REGISTRY_CRED}", passwordVariable: 'D_PASS', usernameVariable: 'D_USER')]) {
                        sh "echo $D_PASS | docker login -u $D_USER --password-stdin"
                        sh "docker push ${DOCKER_IMAGE}:${DOCKER_TAG}"
                        sh "docker push ${DOCKER_IMAGE}:latest"
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo "Deploying to Arbiter VM on port 213"
                    sh """
                        docker stop dvp_01_container || true
                        docker rm dvp_01_container || true
                        docker run -d \
                            --name dvp_01_container \
                            --restart unless-stopped \
                            -p 213:80 \
                            ${DOCKER_IMAGE}:latest
                    """
                }
            }
        }
    }

    post {
        always {
            sh "docker logout"
        }
        success {
            echo "Pipeline completed successfully! Application available at http://192.168.12.203:213"
        }
        failure {
            echo "Pipeline failed. Check Jenkins logs for details."
        }
    }
}



pipeline {
    agent any

    environment {
        IMAGE_NAME = "dhavamani27/docker-jenkins-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                sh 'docker push $IMAGE_NAME:$IMAGE_TAG'
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'docker rm -f mycontainer || true'
                sh 'docker run -d -p 8081:80 --name mycontainer $IMAGE_NAME:$IMAGE_TAG'
            }
        }
    }

    post {
        success {
            echo "CI/CD Pipeline Successful"
        }
        failure {
            echo "Pipeline Failed"
        }
    }
}





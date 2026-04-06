
pipeline {
    agent any

    environment {
        IMAGE_NAME = "ci-cd-app-2"
        PORT = "7550"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Run Container') {
            steps {
                sh """
                docker run -d --name ci-cd-container -p ${PORT}:80 ${IMAGE_NAME}
                """
            }
        }
      
       stage ('Docker Version Info') {
          steps {
            sh 'docker --version'
           }
        }

      stage ('Build number info') {
         steps {
           sh 'Build Number: ${BUILD_NUMBER}'
          }
      }

    }
  }


pipeline {
    agent any

    environment {
        CONTAINER_NAME = 'nestjs-app'
        IMAGE_NAME     = 'nestjs-image'
        EMAIL          = 'shamsherdevp@gmail.com'
        PORT           = '3000'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/shamsherali-devops/CI-CD-PipeLine-using-jenkins-github-webhook-ubuntu-AWS-EC2-Docker'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Stop & Remove Previous Container') {
            steps {
                sh """
                   docker stop ${CONTAINER_NAME} || true
                   docker rm ${CONTAINER_NAME} || true
                """
            }
        }

        stage('Run Docker Container') {
            steps {
                sh """
                   docker run -d -p ${PORT}:${PORT} \
                   --name ${CONTAINER_NAME} ${IMAGE_NAME}
                """
            }
        }

        stage('Send Email Notification') {
            steps {
                emailext(
                    subject: "NestJs app Deploy Successful using Jenkins and Docker on AWS EC2",
                    body: """The NestJs application has been successfully deployed 
                             and is running on port http://13.49.241.233:${PORT}/""",
                    to: "${EMAIL}"
                )
            }
        }
    }
}

pipeline{
  agent any
    environment {
        CONTAINER_NAME = 'nestjs-app'
        IMAGRE_NAME = 'nestjs-image'
        EMAIL= 'shamsherdevp@gmail.com'
        PORT = '3000'
    }

    stages{
        stage('clone repo'){
            steps{
                git branch: 'main',
                url: 'https://github.com/shamsherali-devops/CI-CD-PipeLine-using-jenkins-github-webhook-ubuntu-AWS-EC2-Docker'
      
                
                 }
            

    }
    stage('Build Docker Image'){
        steps{
            sh 'docker build -t $IMAGRE_NAME .'
        }
    }
    }


    stage('Stop & remove previous container'){
        steps{
            sh """
               docker stop $CONTAINER_NMAE || true
               docker rm $CONTAINER_NAME || true
            """
        }
    }


    stage('Docker container run'){
        steps{
            sh """
               docker run -d -p $PORT:$PORT 
               --name $CONTAINER_NAME $IMAGRE_NAME
            """
        }
    }
    
    stage('Send email notification'){
        steps{
            emailtext(
                subject:"NestJs app Deploy Successful using Jenkins and docker on AWS EC2",
                body:"The NestJs application has been successfully deployed and is running on port 
                http://13.49.241.233:${PORT)}/
                ",
                to: "${EMAIL}"   
            
            )
        }
    }
}

pipeline {
  agent any  
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
    stages {
    stage('Build') {
        steps {
        sh 'sudo docker build -t flaskapp:latest .'
        }
    }
    stage('Login') {
        steps {
        sh 'sudo echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
        }
    }
    stage('Push') {
        steps {
        sh 'sudo docker tag flaskapp:latest danyalfaheem/flaskapp:latest'
        sh 'sudo docker push danyalfaheem/flaskapp:latest'
        }
    }
    stage('Execute') {
        steps {
            sh 'sudo kubectl version'
            sh 'sudo kubectl apply -f deployment.yaml'
            sh 'sudo kubectl apply -f service.yaml'
        }
    }
  }
}

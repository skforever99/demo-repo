pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t skforever99/python-app:latest1 .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push skforever99/python-app:latest1'
      }
    }
     stage ('pull'){
      steps { 
            sh 'sudo docker pull skforever99/python-app:latest1 '
           } 
    }
    stage ('deploy'){
      steps {  sh 'sudo docker run -d -p 80:80 skforever99/python-app:latest1' }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
   
  }
}


pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t skforever99/python-app:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push skforever99/python-app:latest'
      }
    }
     stage ('pull'){
      steps { 
            sh 'sudo docker pull skforever99/python-app:latest '
           } 
    }
    stage ('deploy'){
      steps {  sh 'sudo docker run -d -p 80:80 skforever99/python-app:latest' }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
   
  }
}


pipeline {
  environment {
    registry = "akenkour/gsd"
    registryCredential = 'docker-creds'
    dockerImage = ''
  }
  
  agent any
  
  stages {
      
    stage('Cloning Git') {
      steps {
        git 'https://github.com/rakenkou-github/war-build-docker.git'
      }
    }

    stage('Package Maven') {
      steps{
        sh 'echo "Package Maven"'
      }
    }
    /*
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
    */
  }
}

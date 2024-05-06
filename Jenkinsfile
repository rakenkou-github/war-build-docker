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
        sh 'mvn package'
      }
    }
    
    stage('Building image') {
      steps{
        script {
            def img = stage('Build') {
                docker,build("$")
            }
            img.withRun("--name run -$BUILD_ID -p 8081:8081") {
                c -> 
                sh 'docker ps'
            }
        }
      }
    }
    
    /*
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

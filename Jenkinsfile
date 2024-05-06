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

    /*
    stage('Package Maven') {
      steps{
        sh 'mvn package'
      }
    }
    */

    stage('com') {
        steps{
            script{
                def mvnHome = tool name: 'Apache Maven 3.6.0', type: 'maven'
                sh "${mvnHome}/bin/mvn -B -DskipTests clean package"
            }
        }
        
    }
    
    stage('Building image') {
      steps{
        script {
            def registryProjet='https://index.docker.io/v1/akenkour/gsd'
	        def IMAGE="${registryProjet}:version-${env.BUILD_ID}"
	        echo "IMAGE = $IMAGE"
            def img = stage('Build') {
                docker.build("$IMAGE", '.')
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

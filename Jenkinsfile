pipeline {
    agent any 
    environment {
        registry = "sravangcpdocker/toolkit"
        registryCredential = 'dockerhub_id'
        dockerImage = ''
    }
    
    stages {
        stage('Cloning Git') {
            steps {
                sh 'git clone https://github.com/sravan-gc-github/toolkit.git'
                sh 'pwd'
                sh 'cd toolkit'
                sh 'ls -ltr'
            }
        }
    
    // Building Docker images
    stage('Building image') {
      steps{
        script {
            sh 'cp /var/lib/jenkins/workspace/testjob/toolkit/Dockerfile /var/lib/jenkins/workspace/testjob/ '
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    
     // Uploading Docker images into Docker Hub
    stage('Upload Image') {
     steps{    
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
            }
        }
      }
    }
 }

 post {
        always {
            cleanWs deleteDirs: true
        }
     }
}

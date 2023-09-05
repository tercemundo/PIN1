pipeline {
  agent any

  options {
    timeout(time: 2, unit: 'MINUTES')
  }

  environment {
    ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"
  }
   stages {
   stage('Building image') {
      steps{
          sh '''
          docker build -t testapp .
             '''  
        }
    }
  
  
    stage('Run tests') {
      steps {
        sh "docker run testapp npm test"
      }
    }
   stage('Deploy Image') {
      steps{
        sh '''
        docker tag testapp 127.0.0.1:5000/repository/docker/testapp
        docker push 127.0.0.1:5000/repository/docker/testapp
        docker run --rm -v cache:/root/.cache/ aquasec/trivy:0.18.3 192.168.136.128:5000/repository/docker/testapp
        '''
        }
      }
    }
}


    
  


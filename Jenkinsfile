pipeline{
  agent { label 'centos' }
  environment {
    DOCKER_CREDS = credentials('dockercred')
  }
  stages{
    stage('build'){
      steps{
        sh 'docker build . -t zeusequinox/sample-nginx:latest'
        sh 'docker login -u ${DOCKER_CREDS_USR} -p ${DOCKER_CREDS_PSW}'
        sh 'docker pull zeusequinox/sample-nginx:latest'
      }
        
    }
    
    stage('deploy'){
      steps{
        sh 'kubectl delete deployment nginx-worker'
        sh 'kubectl delete service my-service'
        sh 'kubectl create -f nginx-deployment.yaml'
        sh 'kubectl create -f nginx-service.yaml'
      }
    }

  }
 }

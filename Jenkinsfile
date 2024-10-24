pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/kshelp/099', branch: 'master'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        docker build --no-cache -t 192.168.1.10:8443/react-app .
        docker push 192.168.1.10:8443/react-app
        '''
      }
    }
    stage('deploy kubernetes') {
      steps {
        sh '''
        kubectl delete -f service.yaml
        kubectl delete -f deployment.yaml
        kubectl apply -f deployment.yaml
        kubectl apply -f service.yaml
        '''
      }
      
    }
  }
}
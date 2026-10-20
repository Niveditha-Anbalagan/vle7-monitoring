pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t myapp:latest .'
      }
    }
    stage('Load image to Minikube') {
      steps {
        sh 'docker save myapp:latest | docker exec -i minikube docker load'
      }
    }
    stage('Deploy') {
      steps {
        sh 'kubectl apply -f deployment.yaml'
        sh 'kubectl rollout restart deployment/myapp'
        sh 'kubectl rollout status deployment/myapp --timeout=180s'
      }
    }
  }
}

pipeline {
  agent {
    kubernetes {
      yaml '''
spec:
  containers:
  - name: python
    image: python:3.9.15-slim-bullseye
    command:
    - sleep
    - 99d
  terminationGracePeriodSeconds: 3
      '''
      defaultContainer 'python'
      retries 2
    }
  }
  stages {
    stage('Build') {
      steps {
        sh 'pip install -r requirements.txt'
        sh 'python helloworld.py'
      }
    }
  stage('run minikube') {
    steps {
      sh 'echo hello world'
    }
  }
  }
}
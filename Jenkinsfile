pipeline {
  agent {
    kubernetes {
      yaml '''
spec:
  containers:
  - name: python
    image: python:latest
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
    // build the docker image from the source code using the BUILD_ID parameter in image name
      steps {
        sh 'docker build -t python-hello .'
      }
    }
    stage('Run docker') {
      steps {
        sh 'sudo docker run --name python-hello -p 5000:5000 python-hello' 
        }
    }
  }
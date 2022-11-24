pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build'
        sh 'pip install -r requirements.txt'
      }
    }

    stage('Deploy') {
      steps {
        sh 'python helloworld.py'
      }
    }

  }
}
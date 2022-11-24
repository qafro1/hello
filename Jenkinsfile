pipeline {
  agent {
    docker {
      image 'python'
      args '-p 5000:5000 '
    }

  }
  stages {
    stage('Build') {
      steps {
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
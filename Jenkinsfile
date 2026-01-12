pipeline {
  agent any

  options {
    timestamps()
    wrap([$class: 'AnsiColorBuildWrapper', 'colorMapName': 'xterm'])
  }

  environment {
    NODE_ENV = 'test'
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install') {
      steps {
        sh 'npm ci'
      }
    }

    stage('Test') {
      steps {
        sh 'npm test'
      }
    }

    stage('Package') {
      steps {
        sh 'tar -czf artifact.tar.gz .'
        archiveArtifacts artifacts: 'artifact.tar.gz', fingerprint: true
      }
    }

    stage('Deploy') {
      when {
        branch 'main'
      }
      steps {
        sh 'echo "Deploy step placeholder"'
      }
    }
  }

  post {
    success {
      echo 'Pipeline completed successfully!'
    }
    failure {
      echo 'Pipeline failed.'
    }
  }
}

pipeline {
  agent any

  options {
    timestamps()
    ansiColor('xterm')
  }

  environment {
    // Example: NODE_ENV = 'test'
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Setup') {
      steps {
        sh 'node -v || echo "Node not found—ensure Node is installed on the agent"'
        sh 'npm ci'
      }
    }

    stage('Build') {
      steps {
        sh 'npm run build'
      }
    }

    stage('Test') {
      steps {
        sh 'npm test'
      }
      post {
        always {
          junit allowEmptyResults: true, testResults: '**/junit*.xml'
        }
      }
    }

    stage('Package') {
      steps {
        sh 'tar -czf artifact.tar.gz app.js server.js package.json node_modules'
        archiveArtifacts artifacts: 'artifact.tar.gz', fingerprint: true
      }
    }

    stage('Deploy') {
      when {
        branch 'main'
      }
      steps {
        sh '''
          echo "Deploy placeholder—replace with your script"
          # Example: scp artifact.tar.gz user@server:/opt/app/
          # Or docker build/push, or kubectl apply
        '''
      }
    }
  }

  post {
    success {
      echo 'Pipeline succeeded'
    }
    failure {
      echo 'Pipeline failed'
    }
  }
}

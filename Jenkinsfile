pipeline {
  agent any
  stages {
    stage('Build in Docker') {
      agent {
        docker {
          image 'node:16'  // Node.js Docker image
          args '-v /var/run/docker.sock:/var/run/docker.sock'  // Mount Docker socket for Docker commands
        }
      }
      stages {
        stage('Install Dependencies') {
          steps {
            sh 'npm install'
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
        }
        stage('Security Scan') {
          steps {
            sh 'npm install -g snyk'
            sh 'snyk test'
          }
        }
      }
    }
  }
}

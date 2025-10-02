pipeline {
  agent any
  environment {
    // Appends these to the existing PATH safely
    PATH+EXTRA = "/opt/homebrew/bin:/usr/local/bin"
  }
  stages {
    stage('Diagnostics') {
      steps {
        sh 'echo PATH=$PATH'
        sh 'which docker || echo "docker not in PATH"'
        sh 'docker version || true'
      }
    }
    stage('Run Maven in Docker') {
      agent {
        docker {
          image 'maven:3.9.11-eclipse-temurin-21-alpine'
          reuseNode true
        }
      }
      steps {
        sh 'mvn --version'
      }
    }
  }
}

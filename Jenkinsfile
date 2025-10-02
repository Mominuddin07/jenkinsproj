/* Requires the Docker Pipeline plugin */
pipeline {
  agent any
  environment {
    PATH = "/opt/homebrew/bin:/usr/local/bin:${env.PATH}"
  }
  stages {
    stage('Diagnostics') {
      steps {
        sh 'echo PATH=$PATH'
        sh 'which docker || echo "docker not in PATH"'
        sh 'docker version || true'
        sh 'ls -l /var/run/docker.sock || true'
        sh 'id'
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

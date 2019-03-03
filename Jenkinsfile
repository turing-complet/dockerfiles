pipeline {
  agent any
  stages {
    stage('Hello') {
      parallel {
        stage('Hello') {
          steps {
            sh 'echo "Step 1"'
          }
        }
        stage('') {
          steps {
            sh 'docker build cathode -t cathode:test'
          }
        }
      }
    }
  }
}
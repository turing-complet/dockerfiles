pipeline {
  agent {
    dockerfile {
      filename 'cathode/Dockerfile'
    }

  }
  stages {
    stage('Hello') {
      steps {
        sh 'echo "Step 1"'
      }
    }
  }
}
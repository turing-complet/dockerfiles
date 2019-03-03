pipeline {
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('Hello') {
      steps {
        script {
          echo "Starting build cathode"

          def customImage = docker.build("cathode:${env.BUILD_ID}", "cathode")

          customImage.inside {
            echo "build cathode"
          }
        }

      }
    }
  }
}
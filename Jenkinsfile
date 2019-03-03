pipeline {
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('Build and push cathode') {
      steps {
        script {
          echo "Starting build cathode"
          docker.withRegistry('https://jontestregistry.azurecr.io', '92aa84c7-9722-4232-b469-632cae4797a6') {
            def customImage = docker.build("cathode:${env.BUILD_ID}", "cathode")
            customImage.push()
          }
        }

      }
    }
  }
}
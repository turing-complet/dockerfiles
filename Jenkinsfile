pipeline {
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('Build cathode') {
      steps {
        script {
          echo "Starting build cathode"

          def customImage = docker.build("cathode:${env.BUILD_ID}", "cathode")
        }

      }
    }
    stage('Push image') {
      steps {
        script {
          docker.withRegistry('jontestregistry.azurecr.io', '92aa84c7-9722-4232-b469-632cae4797a6')
          customImage.Push()
        }

      }
    }
  }
}
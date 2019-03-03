pipeline {
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('Build dockerfiles') {
      parallel {
        stage('Cathode') {
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
        stage('Xeyes') {
          steps {
            script {
              echo "Starting build xeyes"
              docker.withRegistry('https://jontestregistry.azurecr.io', '92aa84c7-9722-4232-b469-632cae4797a6') {
                def customImage = docker.build("xeyes:${env.BUILD_ID}", "xeyes")
                customImage.push()
              }
            }

          }
        }
      }
    }
  }
}
pipeline {
  agent any
  tools {
        maven 'Maven363'
  stages {
    stage('Build') {
      steps {
        sh "mvn clean install"
      }
    }
  }
}
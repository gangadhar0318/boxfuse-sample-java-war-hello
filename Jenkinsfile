pipeline {
  agent any
  tools {
    maven 'Maven363'
  }
  options {
  buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '5', numToKeepStr: '5')
  }
  stages {
    stage('Build') {
      steps {
        sh "mvn clean install"
      }
    }
  }
}
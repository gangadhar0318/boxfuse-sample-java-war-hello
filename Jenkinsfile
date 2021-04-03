pipeline {
  agent any
  tools {
    maven 'Maven363'
  }
  options {
    timeout(10)
    buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '5', numToKeepStr: '5')
  }
  stages {
    stage('Build') {
      steps {
        sh "mvn clean install"
      }
    }
    post {
      always {
        deleteDir()
      }
      failure {
        echo "send mail -s mvn job failed reciepients@my.com"
      }
      success {
        echo "job is successful"
      }
    }
  }
}
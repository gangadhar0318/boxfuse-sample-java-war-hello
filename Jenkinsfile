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
        echo "send mail -s maven job failed reciepients@mail.com"
      }
      success {
        echo "the job is successful"
      }
    }
  }
}
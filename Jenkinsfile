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
    stage('deploy') {
      steps {
        sshagent(['Deploy_cred']) {
          sh 'scp -o StrictHostKeyChecking=no target/hello-1.0.war ec2-user@10.0.0.104:/opt'
        }
      }
    }
    
  }
  post {
    always{
      deleteDir()
    }
    failure {
      echo "sendmail -s mvn build failed receipients@my.com"
    }
    success {
      echo "The job is successful"
    }
  }
}
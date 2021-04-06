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
      parallel {
        stage('deploy to app server') {
          environment {
           target_user= 'ec2-user'
           target_server= '10.0.0.104'
          }
          steps {
            sshagent(['Deploy_cred']) {
            sh "scp -o StrictHostKeyChecking=no target/hello-1.0.war $target_user@$target_server:/root/devops/apache-tomcat-9.0.44/webapps"
            }
          }
        }
        stage('deploy to dev env') {
          environment {
            target_user= 'ec2-user'
            target_server= '10.0.0.87'
          }
          steps {
            sshagent(['slave1_cred']) {
            sh "scp -o StrictHostKeyChecking=no target/hello-1.0.war $target_user@$target_server:/opt"
            }
          }
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
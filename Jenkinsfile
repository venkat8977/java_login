def tomcatServerUrl = "http://65.2.122.226:8080/"
pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '"mvn" -Dmaven.test.failure.ignore clean install'
      }
    }
    stage('Deploy') {
      steps {   
         deploy adapters: [tomcat8(credentialsId: 'tomcat_credential', path: '', url: 'http://65.2.122.226:8080')], contextPath: 'tomcat', war: '**/**.war'
      }
    }

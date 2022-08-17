
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
         deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://43.205.191.61:8080')], contextPath: 'java_web_application', war: '**/*.war'
      }
    }

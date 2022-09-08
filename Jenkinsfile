pipeline{
  agent any
  stages{
      stage("Scan"){
        steps{
         withSonarQubeEnv(installationName: 'sonarqube-8.9.2', credentialsId: 'sonarqube-token'){
         sh "mvn sonar:sonar"
         }
        }
      }
      stage("Build"){
        steps{
            sh "mvn -B -DskipTests clean package"
            sh "mv target/*.war target/myweb.war"
             }
            }
      stage('Test') {
        steps {
        sh(script: 'mvn -Dmaven.test.failure.ignore test')
      }
      post {
        always {
            junit '**/target/surefire-reports/TEST-*.xml'
             }
           }
      }
      stage("deploy"){
       steps{
          deploy adapters: [tomcat8(credentialsId: 'tomcat-credentials', path: '', url: 'http://172.31.89.145:8080/')], contextPath: 'javaWebApp', war: '**/*.war'          
          }
        }
      }
    }

pipeline {
    
    agent any
    environment {

      sonar_url = 'http://172.31.15.217:9000/'
      sonar_username = 'admin'
      sonar_password = 'admin'
      nexus_url = 'http://172.31.15.217:8081'
      artifact_version = '4.0.0'

 }

    tools {
    jdk 'Java8'
    maven 'maven3.3.9'

  }

    stages {
        
        stage('Git Clone') {
            steps {
                git 'https://github.com/SrideviPutta/gameoflife.git'

            }

        }
        stage('Maven build') {
            steps {
                sh  'mvn clean install'

            }
        }
        stage ('Sonarqube Analysis'){
           steps {
           withSonarQubeEnv('sonarqube') {
           sh '''
           mvn -e -B sonar:sonar -Dsonar.java.source=1.8 -Dsonar.host.url="${sonar_url}" -Dsonar.login="${sonar_username}" -Dsonar.password="${sonar_password}" 
           '''
           }
         }
      }

    }
    
}

pipeline {
    agent {label 'SPC'}
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage ('git checkout') {
            steps {
                git url: 'https://github.com/Sangeeth5/spring-petclinic',
                    branch: 'main'
            }
        }
        stage ('build and scan') {
            steps {
              withCredentials([string(credentialId: 'sonar-id', variable: 'SONAR_TOKEN')]) {
               withSonarQubeEnv('sonar-id') { 
                sh """mvn package sonar:sonar \
                      -Dsonar.projectKey=Sangeeth5_spring-petclinic
                      -Dsonar.organization= sangeeth5 \
                      -Dsonar.host.url= https://sonarcloud.io/ \
                      -Dsonar.login=$SONAR_TOKEN"""
              }
             
              
              }
            }
        }
    }
}
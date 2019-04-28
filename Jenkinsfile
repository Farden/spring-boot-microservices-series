pipeline {
  agent any
  stages {
    stage('scm checout') {
      steps {
        git(url: 'https://github.com/Farden/spring-boot-microservices-series.git', branch: 'master', credentialsId: 'github')
      }
    }
    stage ('Build and Package') {

            steps {
                withMaven(maven : 'maven-3') {
                    sh 'mvn package'
                }
            }
        }
      stage("build & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('sonarqube') {
                sh 'mvn clean package sonar:sonar'
              }
            }
          }
       }
    }
  }
}

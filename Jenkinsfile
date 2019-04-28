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
      stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    // Optionally use a Maven environment you've configured already
                    withMaven(maven:'maven-3') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
         }
      }
  }



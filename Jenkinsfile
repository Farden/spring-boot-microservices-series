pipeline {
  agent any
  stages {
    stage('scm checout') {
      steps {
        git(url: 'https://github.com/Farden/spring-boot-microservices-series.git', branch: 'master')
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
      stage('Slack Message') {
            steps {
                slackSend channel: '#jenkins-build',
                    color: 'good',
                    message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}"
            
            }
         }
      }
  }



pipeline {
  agent any
  stages {
     stage('Tests'){
     steps{
     bat 'gradlew test'
     }
     post {
             success{
             archiveArtifacts 'target/*.json'
             }
     }
     }
     stage('Code Analysis') {
        parallel {
          stage('Code Analysis') {
            steps {
              withSonarQubeEnv('sonar') {
                bat(script: 'gradlew sonarqube', returnStatus: true)
              }

              waitForQualityGate true
            }
          }

          stage('Test Reporting') {
            steps {
              cucumber 'reports/*json'
            }
          }
        }
      }
    stage('build') {
      post {
        failure {
          script {
            mail="Build failed"
          }
        }
        success {
          script {
            mail="Build succeeded"
          }
        }
      }
      steps {
        bat 'gradlew build'
        bat 'gradlew javadoc'
        archiveArtifacts 'build/libs/*.jar'
        junit(testResults: 'build/test-results/test/*.xml', allowEmptyResults: true)
      }
    }
    stage("deploy") {
    steps{
    bat 'gradlew publish'
    }
    }
    stage('Mail Notification') {
        steps {
            mail(subject: 'success notification', body: mail, cc: 'ky_benali@esi.dz', bcc: 'ka_oubahi@esi.dz')
        }
    }
}
}
/*password = quli fgyu nqyi knki*/
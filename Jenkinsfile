pipeline {
agent any
stages{
  stage('Build'){
    steps{
    bat "gradlew build"
    }
    post {
        success{
        archiveArtifacts 'target/*.hpi,target/*.jpi'
        }
    }
  }
  stage('Tests'){
    steps{
        bat "gradlew test"
    }
    post {
        always{
            junit '**/surefire-reports/**/*.xml'
        }
    }

  }
}
}
pipeline {
agent any
stages{
  stage('Build'){
    steps{
    bat "gradlew build"
    }
    post {
        success{
        archiveArtifacts 'target/*.json'
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
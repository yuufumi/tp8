pipeline {
agent any
stages{
  stage('Build'){
    steps{
    bat "gradlew build"
    }
  }
  stage('Tests'){
    steps{
        bat "gradlew test"
    }
    post {
        success{
        archiveArtifacts 'target/*'
        }
    }
  }
}
}
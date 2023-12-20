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
        cucumber buildStatus: 'UNSTABLE',
                        failedFeaturesNumber: 1,
                        failedScenariosNumber: 1,
                        skippedStepsNumber: 1,
                        failedStepsNumber: 1,
                        classifications: [
                                [key: 'Commit', value: '<a href="${GERRIT_CHANGE_URL}">${GERRIT_PATCHSET_REVISION}</a>'],
                                [key: 'Submitter', value: '${GERRIT_PATCHSET_UPLOADER_NAME}']
                        ],
                        reportTitle: 'My report',
                        fileIncludePattern: 'target/*report.json',
                        sortingMethod: 'ALPHABETICAL',
                        trendsLimit: 100
        }
    }
  }
}
}
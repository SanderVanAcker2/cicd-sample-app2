node {
  properties([pipelineTriggers([[$class: 'GitHubPushTrigger']])])
  stage('Preparation') {
    catchError(buildResult: 'SUCCESS') {
      sh 'docker stop samplerunning || true'
      sh 'docker rm samplerunning || true'
    }
  }
  stage('Build') {
    build job: 'BuildSampleApp'
  }
  stage('Results') {
    build job: 'TestSampleApp'
  }
}
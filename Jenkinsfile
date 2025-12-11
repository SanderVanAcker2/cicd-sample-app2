pipeline {
  agent any
  triggers { githubPush() }
  stages {
    stage('Debug SCM') {
      steps {
        echo "ENV: ${env.GIT_BRANCH} ${env.GIT_COMMIT}"
        sh 'git rev-parse --short HEAD || true'
        sh 'git ls-remote origin || true'
      }
    }
    stage('Preparation') {
      steps {
        catchError(buildResult: 'SUCCESS') {
          sh 'docker stop samplerunning || true'
          sh 'docker rm samplerunning || true'
        }
      }
    }
    stage('Build') { steps { build job: 'BuildSampleApp' } }
    stage('Results') { steps { build job: 'TestSampleApp' } }
  }
}
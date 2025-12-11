pipeline {
    agent any
    triggers {
        githubPush()
    }
    stages {
        stage('Preparation') {
            catchError(buildResult: 'SUCCESS') {
                sh 'docker stop samplerunning'
                sh 'docker rm samplerunning'
            }
        }
        stage('Build') {
            steps {
                build job: 'BuildSampleApp'
            }
        }
        stage('Results') {
            steps {
        build job: 'TestSampleApp'
            }
        }
    }
}
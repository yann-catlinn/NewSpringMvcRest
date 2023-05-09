def generateStageReport(stageName, stageResult) {
  def status
  if (stageResult == 'SUCCESS') {
    status = ":white_check_mark: SUCCESS"
  } else {
    status = ":x: FAILURE"
  }

  return "* ${stageName}: ${status}"
}

pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh 'npm install'
        sh 'npm run build'
      }
    }

    stage('Test') {
      steps {
        sh 'npm test'
      }
    }
  }

  post {
    always {
      script {
        def results = []
        for (stage in currentBuild.getStageFlowNodes()) {
          def stageName = stage.getDisplayName()
          def stageResult = stage.getStatus().toString()
          results.add(generateStageReport(stageName, stageResult))
        }

        def summary = "Pipeline summary:\n"
        summary += results.join("\n")
        slackSend channel: '#fundamentos-de-devops', message: summary, tokenCredentialId: 'SecretSlack'
      }
    }
  }
}

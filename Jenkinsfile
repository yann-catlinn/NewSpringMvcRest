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
        for (node in FlowNodes.getNodeList(currentBuild.rawBuild, true)) {
          def stageName = node.getDisplayName()
          def stageResult = node.getStatus().toString()
          results.add(generateStageReport(stageName, stageResult))
        }

        def summary = "Pipeline summary:\n"
        summary += results.join("\n")
        slackSend channel: '#fundamentos-de-devops', message: summary, tokenCredentialId: 'SecretSlack'
      }
    }
  }
}

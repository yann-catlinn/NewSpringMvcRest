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
    stage('Clean') {
      steps {
        sh 'mvn clean'
      }
    }

    stage('Build') {
      steps {
        sh 'mvn install'
      }
    }
  }

  post {
    always {
      script {
        def results = []
        for (run in currentBuild.runs) {
          def stageName = run.parent.name
          def stageResult = run.result.toString()
          results.add(generateStageReport(stageName, stageResult))
        }

        def summary = "Pipeline summary:\n"
        summary += results.join("\n")
        slackSend channel: '#fundamentos-de-devops', message: summary, tokenCredentialId: 'SecretSlack'
      }
    }
  }
}

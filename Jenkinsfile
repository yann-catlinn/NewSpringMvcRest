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
        def results = [:]

        currentBuild.rawBuild.getBuild().getLog(1000).each { line ->
          if (line.contains("[Pipeline] stage")) {
            currentStage = line.substring(line.indexOf("stage ") + 6, line.length() - 2)
          }
          if (line.contains("SUCCESS") || line.contains("FAILURE")) {
            results[currentStage] = line
          }
        }

        def summary = "Pipeline summary:\n"
        results.each { stageName, stageResult ->
          def status = stageResult.contains("SUCCESS") ? ":white_check_mark: SUCCESS" : ":x: FAILURE"
          summary += "* ${stageName}: ${status}\n"
        }

        slackSend channel: '#fundamentos-de-devops', message: summary, tokenCredentialId: 'SecretSlack'
      }
    }
  }
}

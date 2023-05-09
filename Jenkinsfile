library identifier: 'genric.groovy@master', retriever:          modernSCM([$class: 'GitSCMSource', credentialsId: '', remote: 'https://github.com/mani1soni/jenkins-practice.git', traits: [[$class: 'jenkins.plugins.git.traits.BranchDiscoveryTrait']]])
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

    stage('Install') {
      steps {
        sh 'mvn install'
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

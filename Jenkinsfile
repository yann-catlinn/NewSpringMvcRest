pipeline {
    agent any
    
    environment {
    PATH = "C:\\Program Files\\Git\\usr\\bin;C:\\Program Files\\Git\\bin;${env.PATH}"

    stages {
        stage('Initialize'){
            steps{
                echo "PATH = ${MAVEN_HOME}/bin:${PATH}"
                echo "MAVEN_HOME = /opt/maven"
            }
        }
        stage('Build') {
            steps {
                dir("/var/lib/jenkins/workspace/New_demo/") {
                sh 'mvn -B -DskipTests clean package'
                }
            
            }
        }
     }
    post {
    always {
      junit(
        allowEmptyResults: true,
        testResults: '**/test-reports/*.xml'
      )
    }
    }
    }
}

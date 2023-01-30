pipeline {
    agent any
    
    stages {
        stage('Initialize'){
            steps{
                echo "PATH = ${MAVEN_HOME}/bin:${PATH}"
                echo "MAVEN_HOME = /opt/maven"
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'           
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

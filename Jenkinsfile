pipeline { 
     agent any
   
    stages {
        stage('Build') { 
            steps {
                dir("/workspace/MAVEN pipeline/my-app/") {
                sh 'mvn -B -DskipTests clean package'
                }
        }
        stage('Test'){
            steps {
                echo "$PATH" 
                sh 'make check'
                junit 'reports/**/*.xml' 
            }
        }
        stage('Deploy') {
            steps {
                 echo "$PATH"
                sh 'make publish'
            }
        }
    }
     
}

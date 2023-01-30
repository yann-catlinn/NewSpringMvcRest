pipeline { 
     environment {
    PATH = "C:\\Program Files\\Git\\usr\\bin;C:\\Program Files\\Git\\bin;${env.PATH}"
   
    stages {
        stage('Build') { 
            steps { 
                sh 'make' 
            }
        }
        stage('Test'){
            steps {
                sh 'make check'
                junit 'reports/**/*.xml' 
            }
        }
        stage('Deploy') {
            steps {
                sh 'make publish'
            }
        }
    }
     }
}

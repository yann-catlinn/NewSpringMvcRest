pipeline { 
     agent any
   
    stages {
        stage('Build') { 
            steps { 
                echo "$PATH" 
                sh 'make' 
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

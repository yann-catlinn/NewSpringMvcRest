pipeline {
    agent any

       stages {
        stage('Initialize'){
            steps{
                echo "Esta es el inicio"
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B package'
            
            }
        }
        stage ('nexus') {
                steps {
                    script {
                            //pipeline-utility-steps
                       
                            def   pom = readMavenPom file: "pom.xml";
                                nexusArtifactUploader(
                                    nexusVersion: 'nexus3',
                                    protocol: 'http',
                                    nexusUrl: 'localhost:8081/repository/Repositorio1',
                                    groupId: pom.groupId,
                                    version: pom.version,
                                    repository: 'Repositorio1',
                                    credentialsId: 'NexusCredentials',
                                    artifacts: [
                                        [artifactId: pom.artifactId,
                                        classifier: '',
                                        file: 'ROOT.war',
                                        type: pom.packaging]
                                    ]
                                )
                            
                        }   
                }
            } 
     } 
}

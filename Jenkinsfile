pipeline {
    agent any
    
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload War To Nexus'){
            steps{
                script{
                    nexusArtifactUploader artifacts: [
                        [
                            artifactId: 'simple-app', 
                            classifier: '',
                            file: 'target/simple-app-3.0.0.war', 
                            type: 'war'
                        ]
                    ], 
                        credentialsId: 'nexus-jenkins',
                        groupId: 'in.javahome',
                        nexusUrl: '172.31.25.91:8081',
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        repository: 'java-repo-realese',
                        version: '3.0.0'
                    
                }
            }
        }
    }
}

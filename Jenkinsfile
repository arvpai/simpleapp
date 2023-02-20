pipeline {
    agent any
    tools {
        maven 'maven-3.9.0'
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
             }
        }
        stage('Upload War To Nexus')
        {
            steps{
                nexusArtifactUploader artifacts:
                [
                    [
                        artifactId: 'simple-app',
                        classifier: '',
                        file: 'target/simple-app-1.0.0.war',
                        type: 'war'
                    ]
                ],
                        credentialsId: 'nexus3',
                        groupId: 'in.javahome',
                        nexusUrl: '35.89.232.203:8081',
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        repository: 'simpleapp-release',
                        version: '2.0.0'
                }
        }
    }
}
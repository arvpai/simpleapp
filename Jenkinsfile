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
                script{
                    def mavenPom = readMavenPom file: 'pom.xml'
                    def nexusRepoName = mavenPom.version.endsWith("SNAPSHOT") ? "simpleapp-snapshot" : "simpleapp-release"
                nexusArtifactUploader artifacts:
                [
                    [
                        artifactId: 'simple-app',
                        classifier: '',
                        file: "target/simple-app-${mavenPom.version}.war",
                        type: 'war'
                    ]
                ],
                        credentialsId: 'nexus3',
                        groupId: 'in.javahome',
                        nexusUrl: '35.89.232.203:8081',
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        repository: nexusRepoName,
                        version: "${mavenPom.version}"
                    }
                }
        }
    }
}
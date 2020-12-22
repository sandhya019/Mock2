pipeline {
    agent any
    tools {
      maven 'Maven3'
    }
    stages{
        stage('Build'){
            steps{
                sh script: 'mvn clean package'
            }
        }
        stage('Upload jar to Nexus'){
            steps{
                script{
                    def mavenPom = readMavenPom file:'pom.xml'
                    nexusArtifactUploader artifacts: [[
                    artifactId: 'sample',
                    classifier: '',
                    file: "target/*-${mavenPom.version}.jar",
                    type: 'jar']],
                    credentialsId: 'nexus3',
                    groupId: 'com.mycompany',
                    nexusUrl: 'localhost:8081/',
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    repository: Demo_repo,
                    version: "${mavenPom.version}"
                }
            }
        }
    }
}

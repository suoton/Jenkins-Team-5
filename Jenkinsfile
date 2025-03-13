pipeline {
    agent any
    tools{
        maven 'maven-3.9.9'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to tomcat server') {
            steps{
                deploy adapters: [tomcat7(credentialsId: 'tomcat', path: '', url: 'http://13.51.150.96:8080/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}

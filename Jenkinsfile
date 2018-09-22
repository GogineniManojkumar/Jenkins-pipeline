pipeline {
    agent any
    environment {
        MVN_HOME = '/opt/apache-maven-3.5.4'
    }
    tools {
        maven 'LocalMaven'
    }
    stages {
        
        stage('validate-and-compile') {
            steps {
                echo 'Validate and Compile the code'
                sh "mvn clean validate compile"
            }
        }
        stage('code-testing') {
            steps {
                echo 'Testing the code'
                sh "mvn test"
            }
        }
        stage('quality-check') {
            steps {
                echo 'Code Quality Check'
                sh "mvn clean checkstyle:checkstyle"
            }
        }
        stage('build-packaage') {
            steps {
                echo 'Building the war package'
                sh "mvn clean package"
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/*.war', fingerprint: true
                }
            }
        }
    }
}
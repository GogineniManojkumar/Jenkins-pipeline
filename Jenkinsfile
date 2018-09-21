pipeline {
    agent any
    environment {
        MVN_HOME = 'tool name: 'LocalMaven', type: 'maven''
    }
    stages {
        
        stage('validate-and-compile') {
            steps {
                echo 'Validate and Compile the code'
                sh "$MVN_HOME/bin/mvn clean validate compile"
            }
        }
        stage('code-testing') {
            steps {
                echo 'Testing the code'
                sh "$MVN_HOME/bin/mvn test"
            }
        }
        stage('quality-check') {
            steps {
                echo 'Code Quality Check'
                sh "$MVN_HOME/bin/mvn clean checkstyle:checkstyle"
            }
        }
        stage('build-packaage') {
            steps {
                echo 'Building the war package'
                sh "$MVN_HOME/bin/mvn clean package"
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/*.war', fingerprint: true
                }
            }
        }
    }
}
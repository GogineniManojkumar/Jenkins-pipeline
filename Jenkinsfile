pipeline {
    agent any
    stages {
        stage(validate-and-compile) {
            steps {
                echo 'Validate and Compile the code'
                sh 'mvn clean validate compile'
            }
        }
        stage(code-testing) {
            steps {
                echo 'Testing the code'
                sh 'mvn test'
            }
        }
        stage(quality-check) {
            steps {
                echo 'Code Quality Check'
                sh 'mvn clean checkstyle:checkstyle'
            }
        }
        stage(build-packaage) {
            steps {
                echo 'Building the war package'
                sh 'mvn clean package'
                archiveArtifacts artifacts: '**/*.war', fingerprint: true
            }
        }
    }
}
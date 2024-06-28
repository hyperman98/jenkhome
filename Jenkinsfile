pipeline {
    agent { label 'default' }
    options {
        skipStagesAfterUnstable()
    }
    environment {
        JENKINS_URL = "http://91.224.87.113:8080/"
        JSON_FILE = "result.json"
    }
    stages {
        stage('Build') {
            steps {
                sh 'make'
            }
        }
        stage('Test'){
            steps {
                sh 'make check'
                junit 'reports/**/*.xml'
            }
        }
        stage('Deploy') {
            steps {
                sh 'make publish'
            }
        }
    }
}

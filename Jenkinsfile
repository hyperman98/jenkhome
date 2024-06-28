pipeline {
    agent { label 'default' }
    options {
        skipStagesAfterUnstable()
    }
    environment {
        REPO_CREDENTIALS = credentials('last_one2')
        JENKINS_URL = "http://91.224.87.113:8080/"
        JSON_FILE = "result.json"
    }
    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/hyperman98/jenkhome.git', branch: 'main', credentialsId: "${REPO_CREDENTIALS}"
            }
        }
        stage('Deploy') {
            steps {
                sh 'make publish'
            }ho
        }
    }
}

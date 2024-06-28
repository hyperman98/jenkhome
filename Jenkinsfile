pipeline {
    agent { label 'default' }

    parameters {
        string(name: 'USER_NAME', defaultValue: 'World', description: 'Name to greet')
    }

    environment {
        REPO_CREDENTIALS = credentials('last_one2') // Используйте ID ваших креденшалов
    }

    triggers {
        cron('H/5 * * * *') // Запускать каждые 5 минут по расписанию
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
        
        stage('Print Greeting') {
            steps {
                script {
                    def greeting = "Hello ${params.USER_NAME}"
                    writeFile file: 'result.txt', text: greeting
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'result.txt', fingerprint: true
        }
    }
}

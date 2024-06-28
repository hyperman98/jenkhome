pipeline {
    agent { label 'default' }
    options {
        skipStagesAfterUnstable()
    }
    environment {
        REPO_CREDENTIALS = credentials('last_one2')
        JENKINS_URL = "http://91.224.87.113:8080/"
        JSON_FILE = "result.json"
        GIT_REPO = "https://github.com/hyperman98/jenkhome.git"
    }
    stages {
        stage('Build file') {
            steps {
                script {
                    // Получаем информацию о Jenkins
                    def jenkinsInstance = Jenkins.instance
                    def jenkinsVersion = jenkinsInstance.getVersion().toString()
                    def jobName = env.JOB_NAME
                    def buildNumber = env.BUILD_NUMBER

                    // Создаем JSON-объект
                    def buildInfo = [
                        JENKINS_URL: env.JENKINS_URL,
                        JENKINS_VERSION: jenkinsVersion,
                        JOB_NAME: jobName,
                        BUILD_NUMBER: buildNumber
                    ]

                    // Преобразуем JSON-объект в строку
                    def json = new groovy.json.JsonBuilder(buildInfo).toPrettyString()

                    // Записываем JSON-строку в файл
                    writeFile file: env.JSON_FILE, text: json
                }
            }
        }

        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/hyperman98/jenkhome.git', branch: 'main', credentialsId: "${REPO_CREDENTIALS}"
            }
        }
    }
}

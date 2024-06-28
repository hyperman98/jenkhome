pipeline {
    agent { label 'default' }

    environment {
        JENKINS_URL = "http://91.224.87.113:8080/"
        JSON_FILE = "result.json"
        REPO_CREDENTIALS = credentials('last_one2') // Используйте ID ваших креденшалов
    }
    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Connect Repository') {
            steps {
                git url: 'https://github.com/hyperman98/jenkhome.git', branch: 'main', credentialsId: "${REPO_CREDENTIALS}"
            }
        }
        
        stage('Print Greeting') {
            steps {
                script {
                    def jenkinsInstance = Jenkins.instance
                    def jenkinsVersion = jenkinsInstance.getVersion().toString()
                    def jobName = env.JOB_NAME
                    def buildNumber = env.BUILD_NUMBER
                    
                    def result = [
                        JENKINS_URL: env.JENKINS_URL,
                        JENKINS_VERSION: jenkinsVersion,
                        JOB_NAME: jobName,
                        BUILD_NUMBER: buildNumber
                    ]
                    
                    def json = new groovy.json.JsonBuilder(result).toPrettyString()

                    // Записываем JSON-строку в файл
                    writeFile file: env.JSON_FILE, text: json
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'result.json', fingerprint: true
        }
    }
}

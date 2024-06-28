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
                    def jenkinsVersion = sh(script: 'curl -sI ${JENKINS_URL} | grep "X-Jenkins:" | awk \'{print $2}\'', returnStdout: true).trim()
                    def jobName = env.JOB_NAME
                    def buildNumber = env.BUILD_NUMBER
        
                    def result = [
                        JENKINS_URL: env.JENKINS_URL,
                        JENKINS_VERSION: jenkinsVersion,
                        JOB_NAME: jobName,
                        BUILD_NUMBER: buildNumber
                    ]
                    
                     // Создаем JSON вручную с помощью shell команды
                    sh """
                    echo '{
                      "JENKINS_URL": "${env.JENKINS_URL}",
                      "JENKINS_VERSION": "${jenkinsVersion}",
                      "JOB_NAME": "${jobName}",
                      "BUILD_NUMBER": "${buildNumber}"
                    }' > ${env.JSON_FILE}
                    """
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

pipeline {
    agent any

    options {
        timestamps()
        timeout(time: 5, unit: 'MINUTES')
    }

    triggers {
        pollSCM('H/2 * * * *')
    }

    environment {
        GREETING = 'Hello'
    }

    parameters {
        string(name: 'WHO', defaultValue: 'Jenkins', description: 'Кого приветствуем')
    }

    stages {
        stage('Info') {
            steps {
                echo "${GREETING}, ${params.WHO}!"
                sh 'whoami && hostname && pwd'
            }
        }

        stage('Work') {
            steps {
                sh '''
                    echo "build number: $BUILD_NUMBER"
                    echo "hello" > result.txt
                '''
            }
        }

        stage('Parallel') {
            parallel {
                stage('A') { steps { sh 'sleep 3 && echo A done' } }
                stage('B') { steps { sh 'sleep 5 && echo B done' } }
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'result.txt'
            }
        }
    }

    post {
        success { echo 'Всё прошло успешно' }
        failure { echo 'Сборка упалasdа' }
        always  { echo 'Выполняется всегда' }
    }
}

pipeline {
    agent any
    
    stages {
        stage('Проверка Git') {
            steps {
                echo 'Код успешно скачан из GitHub!'
                // Выведем список файлов, чтобы убедиться, что Jenkins видит наш проект
                sh 'ls -la'
                sh 'docker --version' 
            }
        }
    }
}

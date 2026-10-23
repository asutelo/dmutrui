pipeline {
    agent {
        docker { 
            image 'gcc:latest' 
        }
    }
    
    stages {
        stage('Проверка кода (Lint)') {
            steps {
                echo 'Проверяем, что исходный код на месте...'
                sh 'test -f main.c'
            }
        }
        
        stage('Сборка приложения (Build)') {
            steps {
                echo 'Компиляция файла main.c...'
                sh 'gcc main.c -o app'
            }
        }
        
        stage('Интеграционные тесты (Test)') {
            steps {
                echo 'Запуск тестов работоспособности...'
                sh 'chmod +x test.sh'
                sh './test.sh'
            }
        }
    }
}

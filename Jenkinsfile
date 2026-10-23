pipeline {
    agent {
        docker { 
            image 'alpine:latest'
	    args '-u root -v /opt/prod_app:/opt/prod_app' 
        }
    }
    
    stages {
	stage('Подготовка окроужения') {
	    steps {
		echo 'Установка компилятора'
		sh 'apk add --no-cache build-base bash'
	    }
	}

        stage('Проверка кода') {
            steps {
                echo 'Проверяем, что исходный код на месте...'
                sh 'test -f main.c'
            }
        }
        
        stage('Сборка приложения (Build)') {
            steps {
                echo 'Компиляция файла main.c...'
                sh 'gcc -static main.c -o app'
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

    post {
        success {
            echo 'Пайплайн успешно завершился'
            sh 'cp app /opt/prod_app/'
	    echo 'Артефакт скопирован'
	}
	failure {
	    echo 'Пайплайн завершился с ошибкой'
	}
    }
}

pipeline {
    agent any

    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
        ANSIBLE_FORCE_COLOR = 'true'
    }

    stages {
        stage('Подготовка окружения') {
            steps {
                echo '=== Stage 1: Установка Docker/Compose и клонирование репозиториев ==='
                sshagent(credentials: ['ssh-ansible-credentials']) {
                    sh '''
                        ansible-playbook ansible/firstPlaybook.yml -i ansible/inventory --tags "install,deploy"
                    '''
                }
            }
        }

        stage('Запуск приложений') {
            steps {
                echo '=== Stage 2: Запуск микросервисов через docker compose ==='
                sshagent(credentials: ['ssh-ansible-credentials']) {
                    sh '''
                        ansible-playbook ansible/firstPlaybook.yml -i ansible/inventory --tags "start"
                    '''
                }
            }
        }
    }

    post {
        success { echo ' Пайплайн успешен: микросервисы запущены.' }
        failure { echo ' Ошибка. Смотри Console Output.' }
    }
}
pipeline {
    agent any

    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }

    stages {
        stage('Подготовка окружения') {
            steps {
                script {
                    echo '=== Stage 1: install Docker/Compose + clone repos ==='
                    ansiblePlaybook(
                        playbook:      'ansible/firstPlaybook.yml',
                        inventory:     'ansible/inventory',
                        credentialsId: 'ssh-ansible-credentials',
                        tags:          'install,deploy',
                        colorized:     true,
                        become:        true
                    )
                }
            }
        }

        stage('Запуск приложений') {
            steps {
                script {
                    echo '=== Stage 2: docker compose up ==='
                    ansiblePlaybook(
                        playbook:      'ansible/firstPlaybook.yml',
                        inventory:     'ansible/inventory',
                        credentialsId: 'ssh-ansible-credentials',
                        tags:          'start',
                        colorized:     true,
                        become:        true
                    )
                }
            }
        }
    }

    post {
        success { echo 'Пайплайн успешен: микросервисы запущены.' }
        failure { echo 'Ошибка. Смотри Console Output.' }
    }
}
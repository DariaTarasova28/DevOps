node {
    checkout scm
    
    stage('Подготовка окружения') {
        echo '=== Stage 1: Установка Docker/Compose и клонирование репозиториев ==='
        sh '''
            export ANSIBLE_HOST_KEY_CHECKING=False
            ansible-playbook ansible/firstPlaybook.yml -i ansible/inventory --tags "install,deploy" --private-key /var/jenkins_home/jenkins_ansible
        '''
    }

    stage('Запуск приложений') {
        echo '=== Stage 2: Запуск микросервисов через docker compose ==='
        sh '''
            export ANSIBLE_HOST_KEY_CHECKING=False
            ansible-playbook ansible/firstPlaybook.yml -i ansible/inventory --tags "start" --private-key /var/jenkins_home/jenkins_ansible
        '''
    }
}

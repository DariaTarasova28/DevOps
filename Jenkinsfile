node {
    stage('Подготовка окружения') {
        echo '=== Stage 1: Установка Docker/Compose и клонирование репозиториев ==='
        withCredentials([sshUserPrivateKey(credentialsId: 'ssh-ansible-credentials', keyFileVariable: 'SSH_KEY')]) {
            sh 'ansible-playbook ansible/firstPlaybook.yml -i ansible/inventory --tags "install,deploy" --private-key $SSH_KEY'
        }
    }

    stage('Запуск приложений') {
        echo '=== Stage 2: Запуск микросервисов через docker compose ==='
        withCredentials([sshUserPrivateKey(credentialsId: 'ssh-ansible-credentials', keyFileVariable: 'SSH_KEY')]) {
            sh 'ansible-playbook ansible/firstPlaybook.yml -i ansible/inventory --tags "start" --private-key $SSH_KEY'
        }
    }
}
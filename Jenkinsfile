pipeline {
    agent any

    stages {
        stage('Bootstrap Uyuni') {
            steps {
                ansiblePlaybook(
                    playbook: '/root/ansible-uyuni/playbooks/bootstrap.yml',
                    inventory: '/root/ansible-uyuni/inventory.ini',
                    installation: 'Ansible',
                    credentialsId: env.ANSIBLE_CREDENTIALS_ID
                )
            }
        }
    }

    post {
        success {
            echo '✅ Bootstrap terminé avec succès !'
        }
        failure {
            echo '❌ Erreur pendant le bootstrap !'
        }
    }
}

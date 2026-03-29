pipeline {
    agent any

    environment {
        UYUNI_PASSWORD = credentials('uyuni-password')
    }

    stages {
        stage('Bootstrap Uyuni') {
            steps {
                ansiblePlaybook(
                    playbook: '/root/ansible-uyuni/playbooks/bootstrap.yml',
                    inventory: '/root/ansible-uyuni/inventory.ini',
                    installation: 'Ansible',
                    credentialsId: 'ansible-ssh',
                    extraVars: 'uyuni_password=${UYUNI_PASSWORD}'
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

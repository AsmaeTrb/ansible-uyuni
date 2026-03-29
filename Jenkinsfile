pipeline {
    agent any

    stages {
        stage('Bootstrap Uyuni') {
            steps {
                sh '''
                ansible-playbook -i /root/ansible-uyuni/inventory.ini /root/ansible-uyuni/playbooks/bootstrap.yml
                '''
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

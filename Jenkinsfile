pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Bootstrap Uyuni') {
            steps {
                sshagent(credentials: ['ansible-ssh']) {
                    sh '''
                        ansible-playbook -i inventory.ini playbooks/assign_groups.yml
                    '''
                }
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

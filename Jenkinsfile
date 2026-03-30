pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Test SSH') {
            steps {
                sshagent(credentials: ['ansible-ssh']) {
                    sh '''
                        echo "=== Test SSH vers VM2 ==="
                        ssh -o StrictHostKeyChecking=no root@192.168.78.136 "hostname"
                    '''
                }
            }
        }

        stage('Bootstrap Uyuni') {
            steps {
                sshagent(credentials: ['ansible-ssh']) {
                    sh '''
                        ansible-playbook -i inventory.ini playbooks/bootstrap.yml
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

pipeline {
    agent any
    environment {
        VAULT_ADDR = 'http://127.0.0.1:8200'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo "✅ Code récupéré depuis Git"
            }
        }
        stage('Bootstrap Uyuni') {
            steps {
                withCredentials([string(credentialsId: 'vault-token', variable: 'VAULT_TOKEN')]) {
                    sshagent(credentials: ['ansible-ssh']) {
                        sh '''
                            ansible-playbook -i inventory.ini playbooks/bootstrap.yml
                        '''
                    }
                }
            }
        }
        stage('Assign Groups') {
            steps {
                withCredentials([string(credentialsId: 'vault-token', variable: 'VAULT_TOKEN')]) {
                    sh '''
                        ansible-playbook playbooks/assign_groups.yml
                    '''
                }
            }
        }
    }
    post {
        success {
            echo '✅ Bootstrap et groupes terminés avec succès !'
        }
        failure {
            echo '❌ Erreur pendant le pipeline !'
        }
    }
}

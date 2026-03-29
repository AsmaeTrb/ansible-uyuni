pipeline {
    agent any

    environment {
        UYUNI_PASSWORD = credentials('uyuni-password')
    }

    stages {
        stage('Bootstrap Uyuni') {
            steps {
                withEnv(["ANSIBLE_EXTRA_VARS=uyuni_password=${UYUNI_PASSWORD}"]) {
                    sh '''
                    ansible-playbook \
                        -i /root/ansible-uyuni/inventory.ini \
                        /root/ansible-uyuni/playbooks/bootstrap.yml \
                        -e "uyuni_password=${UYUNI_PASSWORD}"
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

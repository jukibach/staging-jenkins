pipeline {

    agent{
        docker {
            image 'alpinelinux/ansible'
        }
    }
    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }
    stages {

        stage('Deploy PostgreSQL container') {
           
            steps {
                withCredentials([file(credentialsId: 'staging_ansible_key', variable: 'staging_ansible_key')]) {
                    sh 'ls -la'
                    sh "cp /$staging_ansible_key staging_ansible_key"
                    sh 'cat staging_ansible_key'
                    sh 'ansible --version'
                    sh 'ls -la'
                    sh 'chmod 400 staging_ansible_key '
                    sh 'ansible-playbook -i hosts --private-key staging_ansible_key playbook.yml'
            }
            }
        }
        
    }
    post {
        // Clean after build
        always {
            cleanWs()
        }
    }
}
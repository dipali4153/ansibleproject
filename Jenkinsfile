pipeline {
    agent any

    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }

    stages {

        stage('Clone Latest Code') {
            steps {

                git branch: 'master',
                    credentialsId: 'github-creds',
                    url: 'https://github.com/dipali4153/ansibleproject.git'
            }
        }

        stage('Check Ansible Version') {
            steps {
                sh 'ansible --version'
            }
        }

        stage('Run Ansible Playbook') {
            steps {

                sshagent(credentials: ['ansible-server-key']) {

                    sh '''
                    ansible-playbook -i ansible/hosts ansible/deploy.yml
                    '''
                }
            }
        }
    }

    post {

        success {
            echo 'Deployment Successful'
        }

        failure {
            echo 'Deployment Failed'
        }
    }
}

pipeline {
    agent any

    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }

    stages {

        stage('Clone Latest Code') {
            steps {

                git branch: 'master',
                url: 'https://github.com/dipali4153/ansibleproject.git'
            }
        }

        stage('Run Ansible Playbook') {
            steps {

                sshagent(['ansible-server-key']) {

                    sh '''
                    ansible-playbook -i ansible/hosts ansible/deploy.yml
                    '''
                }
            }
        }
    }
}

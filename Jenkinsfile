
pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhup')  
        GITHUB_CREDENTIALS = credentials('github-cred')  
    }

    stages {
        stage('Git Clone') {  
            steps {
                script {
                    sh '''
                        git clone https://${GITHUB_CREDENTIALS_USR}:${GITHUB_CREDENTIALS_PSW}@github.com/Mohamedfathy43/Final-Project-orange.git
                    '''
                }
                sh 'ls -la Final-Project-orange'
                sh 'cd Final-Project-orange'
            }
        }
        
        
        stage('Docker Login') {
            steps {
                script {
                    sh '''
                        echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin
                    '''
                }
            }
        }
        
        stage('Run SSH Command') {
            steps {
                script {
                    sh '''
                        ssh -i /var/lib/jenkins/.ssh/id_rsa deployer@192.168.83.144 "uptime"
                    '''
                }
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh '''
                cd Final-Project-orange
                docker build -t mohamedfathy23/web-app .
                '''
            }
        }

        stage('Push Docker Image') {
            steps {
                sh '''
                docker push mohamedfathy23/web-app
                '''
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh '''
    
                export ANSIBLE_HOST_KEY_CHECKING=False
                
                
                ansible-playbook -i /etc/ansible/hosts /etc/ansible/ansible-playbook.yml 
                '''
            }
        }

        
    }
}

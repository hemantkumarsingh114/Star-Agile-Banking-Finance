pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout code from the Git repository
                git url: 'https://github.com/hemantkumarsingh114/Star-Agile-Banking-Finance.git', branch: 'master'
            }
        }
        stage('Build Maven') {
            steps {
                // Run Maven build
                sh 'mvn clean install'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    sh 'docker build -t hemantkumarsingh114/capstoneproject:1.0 .'
                }
            }
        }
        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    script {
                        // Log in to Docker Hub and push the image
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push hemantkumarsingh114/capstoneproject:1.0'
                    }
                }
            }
        }
        stage('Configure Ansible and Deploy to the Test Server') {
            steps {
                ansiblePlaybook(
                    become: true,
                    credentialsId: 'ansible-key1',
                    disableHostKeyChecking: true,
                    installation: 'ansible',
                    inventory: '/etc/ansible/hosts',
                    playbook: 'ansible-playbook.yml'
                )
            }
        }
    }
}

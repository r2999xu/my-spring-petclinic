pipeline {
    agent any
    tools {
     maven 'Maven'
    }


    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/r2999xu/my-spring-petclinic.git'
            }
        }

        stage('Build Application') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Deploy Application') {
            steps {
                sh 'ansible-playbook -i /var/jenkins_home/ansible_hosts deploy_petclinic.yml'
            }
        }
    }
}

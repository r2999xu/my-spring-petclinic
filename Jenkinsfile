pipeline {
    agent any
    tools {
        jdk 'JDK 20'
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
                script {
                    // Get the host's IP address
                    def hostIP = sh(returnStdout: true, script: 'ip route get 1 | awk \'{print $NF;exit}\'').trim()
                    echo "Host IP: ${hostIP}"

                    // Generate a temporary Ansible inventory file
                    writeFile file: 'ansible_hosts', text: "[web]\n${hostIP} ansible_connection=docker ansible_docker_extra_args='-H tcp://localhost:2375' ansible_user=root"

                    // Run the Ansible playbook
                    sh 'ansible-playbook -i ansible_hosts deploy_petclinic.yml'
                }
            }
        }
    }
}

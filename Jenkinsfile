pipeline {
  agent any

  tools {
    jdk 'JDK 20'
    maven 'Maven'
  }

  stages {
    stage('Build') {
      steps {
        sh './mvnw clean install'
      }
    }

    stage('SonarQube analysis') {
      steps {
        withSonarQubeEnv('SonarQube') {
          sh './mvnw sonar:sonar -Dsonar.host.url=http://localhost:9000 -Dsonar.login=admin -Dsonar.password=admin'
        }
      }
    }
  }
}


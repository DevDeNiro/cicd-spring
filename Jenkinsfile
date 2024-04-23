pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Jukiyoomi/cicd-spring.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('To be replaced') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }
    post {
         always {
            junit '**/target/surefire-reports/*.xml'
        }
        success {
            echo 'Build succeeded'
        }
        failure {
            echo 'Build failed'
        }
    }
}

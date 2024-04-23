pipeline {
    agent any

    tools {
<<<<<<< HEAD
        maven 'Maven' // Utilise la version par défaut de Maven
        jdk 'JDK' // Utilise la version par défaut de JDK
    }

    stages {
=======
        maven 'Maven'
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
>>>>>>> 2373e8c (update JenkinsFile with Build, Test & Sonar)
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

pipeline {
    agent any

    tools {
        maven 'Maven' // Utilise la version par défaut de Maven
//         jdk 'JDK' // Utilise la version par défaut de JDK
    }

    stages {
        stage('Test') {
            agent {
                docker { image 'openjdk:8-jdk' }
            }
            steps {
                sh 'mvn test'
            }
        }
    }
}
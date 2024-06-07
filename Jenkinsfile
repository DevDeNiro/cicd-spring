pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/DevDeNiro/cicd-spring.git'
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
        stage('SonarQube Code Analysis') {
            steps {
                dir("${WORKSPACE}"){
                // Run SonarQube analysis for Python
                script {
                    def scannerHome = tool name: 'sonar', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                    withSonarQubeEnv('sonar') {
                        sh "echo $pwd"
                        sh "mvn sonar:sonar \
                              -Dsonar.projectKey=com.example:testing-web-complete \
                              -Dsonar.host.url=http://172.19.0.4:9000 \
                              -Dsonar.login=squ_2bdf6703ead1f5d478b44f3f9e9be4e99d3a70b5"
                    }
                }
            }
            }
        }
        stage("SonarQube Quality Gate Check") {
            steps {
                script {
                    def qualityGate = waitForQualityGate()

                    if (qualityGate.status != 'OK') {
                        echo "${qualityGate.status}"
                        error "Quality Gate failed: ${qualityGateStatus}"
                    }
                    else {
                        echo "${qualityGate.status}"
                        echo "SonarQube Quality Gates Passed"
                    }
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

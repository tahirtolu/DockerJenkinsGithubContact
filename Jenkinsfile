pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/tahirtolu/YMG-Final.git'
            }
        }
        
        stage('Build') {
            steps {
                script {
                    docker.image('maven:3.8.1-jdk-11').inside('-v /var/run/docker.sock:/var/run/docker.sock') {
                        sh 'mvn clean install'
                    }
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    docker.image('maven:3.8.1-jdk-11').inside('-v /var/run/docker.sock:/var/run/docker.sock') {
                        sh 'mvn test'
                    }
                }
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline completed!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}

pipeline {
    agent any
    
    tools {
        // Maven tool configuration
        maven 'maven'
    }
    
    stages {
        stage('Checkout') {
            steps {
                // GitHub'dan proje klonlama
                git branch: 'master', url: 'https://github.com/tahirtolu/YMG-Final.git'
            }
        }
        
        stage('Build Maven') {
            steps {
                // Proje dizinine geçiş yap
                dir('your-project-directory') {
                    // Maven ile proje derleme
                    bat 'mvn clean install'
                }
            }
        }
        
        stage('Stop and Remove Existing Container') {
            steps {
                // Önceki Docker konteyneri durdurma ve kaldırma işlemleri
                script {
                    bat 'docker stop demo-container'
                    bat 'docker rm demo-container'
                }
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // Docker imajını oluşturma işlemi
                script {
                    docker.build("demo13:${env.BUILD_NUMBER}")
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                // Docker konteynerini çalıştırma işlemi
                script {
                    docker.image("demo13:${env.BUILD_NUMBER}").run("-d -p 3030:3030 --name demo-container")
                }
            }
        }
        
        stage('Push Image to Hub') {
            steps {
                // Docker imajını Docker Hub'a gönderme işlemi (Opsiyonel)
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        docker.image("demo13:${env.BUILD_NUMBER}").push()
                    }
                }
            }
        }
    }
}

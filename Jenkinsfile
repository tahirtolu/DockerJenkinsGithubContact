pipeline {
    agent any
    
    environment {
        dockerImage = 'your-custom-docker-image' // Özel Docker imajınızın adı veya ID'si
    }
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-username/your-repo.git'
            }
        }
        
        stage('Build and Test') {
            steps {
                script {
                    docker.image(dockerImage).inside {
                        // Özel build komutlarınızı buraya ekleyin
                        sh 'echo "Building and testing your application"'
                        sh 'ls -al' // Örnek bir komut
                    }
                }
            }
        }
        
        stage('Package') {
            steps {
                script {
                    docker.image(dockerImage).inside {
                        // Özel paketleme komutlarınızı buraya ekleyin
                        sh 'echo "Packaging your application"'
                    }
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    docker.image(dockerImage).inside {
                        // Özel dağıtım komutlarınızı buraya ekleyin
                        sh 'echo "Deploying your application"'
                    }
                }
            }
            
            post {
                success {
                    echo 'Deployment successful!'
                    // Başarı durumunda ek işlemler
                }
                failure {
                    echo 'Deployment failed!'
                    // Hata durumunda ek işlemler
                }
            }
        }
    }
}

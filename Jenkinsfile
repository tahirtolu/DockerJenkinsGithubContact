pipeline {
    agent {
        docker {
            image 'docker:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    environment {
        DOCKER_IMAGE = 'your-dockerhub-username/your-image-name:tag'
    }
    stages {
        stage('Clone Repository') {
            steps {
                // GitHub reposunu klonlama
                git 'https://github.com/tahirtolu/YMG-Final.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                // Docker image'ını build etme
                script {
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }
        stage('Run Container') {
            steps {
                // Docker container'ı çalıştırma
                script {
                    def app = docker.image("${DOCKER_IMAGE}")
                    app.run("-p 8080:8080 -p 4848:4848")
                }
            }
        }
    }
    post {
        always {
            // Her zaman çalışacak adımlar
            echo 'Pipeline completed!'
        }
        success {
            // Başarı durumunda çalışacak adımlar
            echo 'Pipeline başarıyla tamamlandı!'
        }
        failure {
            // Hata durumunda çalışacak adımlar
            echo 'Pipeline başarısız oldu!'
        }
    }
}

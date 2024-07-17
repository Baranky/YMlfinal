pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // GitHub'dan kodları checkout et
                git branch: 'main', url: 'https://github.com/Baranky/YMlfinal.git'
            }
        }

        stage('Stop and Remove Existing Container') {
            steps {
                script {
                    // Varolan container'ı durdur ve sil
                    bat 'docker stop demo-container || exit 0'
                    bat 'docker rm demo-container || exit 0'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Docker image'ını oluştur
                    bat 'docker build -t demo/app:%BUILD_NUMBER% build/web'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Docker container'ı çalıştır
                    bat 'docker run -d -p 9090:8080 --name demo-container demo/app:%BUILD_NUMBER%'
                }
            }
        }
    }
}
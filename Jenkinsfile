pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Bu aşamada Docker imajınızı oluşturun
                script {
                    docker.build('my-node-app:latest', '-f Dockerfile .')
                }
            }
        }
        stage('Test') {
            steps {
                // Testleri burada çalıştırabilirsiniz
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                // Docker imajını Docker registry'ye push etmek için Docker Hub kullanıyoruz, burayı kendi Docker Registry'nize göre değiştirebilirsiniz
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        docker.image('my-node-app:latest').push('latest')
                    }
                }
            }
        }
    }
}

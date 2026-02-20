pipeline {
    agent any

    stages {

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t backend-app backend'
            }
        }

        stage('Remove Old Containers') {
            steps {
                sh 'docker rm -f backend1 backend2 nginx || true'
            }
        }

        stage('Run Backend Containers') {
            steps {
                sh '''
                docker run -d --name backend1 backend-app
                docker run -d --name backend2 backend-app
                '''
            }
        }

        stage('Build Nginx Image') {
            steps {
                sh 'docker build -t nginx-lb nginx'
            }
        }

        stage('Run Nginx') {
            steps {
                sh 'docker run -d -p 8081:80 --name nginx nginx-lb'
            }
        }
    }
}

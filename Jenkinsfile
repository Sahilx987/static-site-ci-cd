pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Sahi/static-site-ci-cd.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t static-site .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                  docker rm -f static-site || true
                  docker run -d -p 8081:80 --name static-site static-site
                '''
            }
        }

        stage('Verify') {
            steps {
                sh 'curl http://localhost:8081'
            }
        }
    }
}


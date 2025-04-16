pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-custom-site"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: "${env.BRANCH_NAME}", url: 'https://github.com/VenkateshGollapudi/cicdjenkins'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $IMAGE_NAME .'
                }
            }
        }

        stage('Deploy if Master') {
            when {
                branch 'master'
            }
            steps {
                script {
                    sh 'docker run -d -p 82:80 --name live-site $IMAGE_NAME'
                }
            }
        }
    }
}

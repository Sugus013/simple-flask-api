pipeline {
    agent any

    environment {
        IMAGE_NAME = 'gantangdev/simple-flask-api' // ganti sesuai Docker Hub lo
        DOCKER_CRED = 'dockerhub-creds' // buat credential ini di Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/gantangdev/simple-flask-api.git' // ganti ke repo kamu
            }
        }

        stage('Unit Test') {
            steps {
                sh 'pip install -r requirements.txt && pytest test_app.py'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: "$DOCKER_CRED", usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh '''
                        echo "$PASS" | docker login -u "$USER" --password-stdin
                        docker push $IMAGE_NAME
                    '''
                }
            }
        }
    }
}

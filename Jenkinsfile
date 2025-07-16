pipeline {
    agent any

    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
    IMAGE_NAME = 'sugus12/simple-flask-api'
}

stages {
    stage('checkout') {
        steps {
            git credentialsId: 'github-creds', url: 'https://github.com/Sugus013/simple-flask-api.git', branch: 'main'
        }
    }

    stage('Docker Build') {
        steps {
            sh 'docker build -t $IMAGE_NAME:latest .'
        }
    }

    stage('Push to Docker Hub') {
        steps {
            withDockerRegistry([credentialsId: 'dockerhub-creds']) {
                sh 'docker push $IMAGE_NAME:latest'
            }
        }
    }
}

}

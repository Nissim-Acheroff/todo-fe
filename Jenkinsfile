pipeline {
    agent any

    stages {
        stage('Build stage') {
            steps {
              sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines -t image-builder --target builder .'
            }
        }
        stage('Test stage') {
            steps {
              sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines -t image-testing --target testing .'
            }
        }
        stage('Delivery stage') {
            steps {
                sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines -t nissimacheroff/todo-fe:$BUILD_NUMBER --target delivery .'
            }
        }
        stage('push') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'docker-pwd')]) {
                    sh "docker login -u nissimacheroff -p  ${docker-pwd}"
                }
                    sh "docker push nissimacheroff/todo-fe:latest"
        }
    }
}
}

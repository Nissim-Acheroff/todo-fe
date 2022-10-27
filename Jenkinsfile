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
                    sh "docker login -u nissimacheroff -p S_i)C(7XnrVap2X
                    sh "docker push nissimacheroff/todo-fe:$BUILD_NUMBER"
        }
    }
}
}

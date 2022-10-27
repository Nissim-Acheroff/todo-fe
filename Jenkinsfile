pipeline {
    agent any
    stages {
        stage('initws & prune') {
            steps {
                cleanWs()
            }
        }
        stage('Build stage') {
            steps {
              sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines  -t build-test:$BUILD_NUMBER --target builder .'
            }
        }
        stage('Test stage') {
            steps {
              sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines -t build-test:$BUILD_NUMBER --target test .'
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
                    sh "docker push nissimacheroff/todo-fe:latest"
            }
        }
    }
}
}


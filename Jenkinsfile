pipeline {
    agent any
    stages {
        stage('initws & prune') {
            steps {
                cleanWs()
            }
        }

        stage('build') {
            steps { 
                sh "pwd" 
                sh "DOCKER_BUILDKIT=1 docker build -t build-image -f docker-pipeline-fe --target builder ."
                
                
            }
        }
        stage('testing') {
            steps { 
                sh "DOCKER_BUILDKIT=1 docker build -t build-testing  --target testing -f docker-pipeline-fe ./todo-fe"
                
                
            }
        }

         stage('delivery') {
            steps { 
                sh "DOCKER_BUILDKIT=1 docker build -t build-delivery --target delivery-f docker-pipeline-fe ./todo-fe"
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

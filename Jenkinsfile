pipeline {
    agent any
    environment {
        DOCKERHUB_USER = "mohammed102003"
        IMAGE_TAG = "${env.BUILD_NUMBER}"
    }
    stages {
        stage("Checkout") {
            steps {
                git branch: "main", url: "https://github.com/mohammedhamdy102003/nodejs-docker-app"
            }
        }
        stage("Build Image") {
            steps {
                sh "docker build -t ${DOCKERHUB_USER}/nodejs-docker-app:${IMAGE_TAG} ."
            }
        }
 stage("Test") {
    steps {
        sh "docker run --rm ${DOCKERHUB_USER}/nodejs-docker-app:${IMAGE_TAG}"
    }
}

        stage("Login to Docker Hub") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-user', usernameVariable: 'DOCKER_HUB_CREDENTIALS_USR', passwordVariable: 'DOCKER_HUB_CREDENTIALS_PSW')]) {
                    sh "echo \$DOCKER_HUB_CREDENTIALS_PSW | docker login -u \$DOCKER_HUB_CREDENTIALS_USR --password-stdin"
                }
            }
        }
        stage("Push Image") {
            steps {
                sh "docker push ${DOCKERHUB_USER}/nodejs-docker-app:${IMAGE_TAG}"
            }
        }
    }
}

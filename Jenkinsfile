pipeline{
    agent any
    environment{
        DOCKER_HUB_CREDENTIALS= credentials("dockerhub-user")
        DOCKERHUB_USER= "mohammed102003"
        IMAGE_TAG= $(env.BUILD_NUMBER)

    }
    stages{
        stage("checkout"){
            steps{
                git branch: "main", url: "https://github.com/mohammedhamdy102003/nodejs-docker-app"
            }
        }
        stage("build image"){
            steps{
                sh "docker build -t $DOCKERHUB_USER/nodejs-docker-app:$IMAGE_TAG"
            }
        }
        stage("test"){
            steps{
             sh "docker run --rm ${IMAGE_NAME}:${IMAGE_TAG} node app.js"
            }
        }
        stage("login to docker hub"){
            steps{
                sh "echo $DOCKER_HUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_USER --password-stdin"
            }
        }
        stage("push image"){
            sh " docker push $DOCKERHUB_USER/nodejs-docker-app:$IMAGE_TAG "
        }
    }
}
@Library("shared") _
pipeline {
    agent { label "ubuntu" }

    stages {
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        stage("Code") {
            steps {
                script{
                    clone("https://github.com/sanskar-devops2620/django-notes-app.git", "main")
                }

            }
        }

        stage("Build") {
            steps {
                script{
                    docker_build("notes-app", "latest", "sanskarwhizhack")
                }

            }
        }

        stage("Test") {
            steps {
                echo "This is testing a code"
                // Add your test script here
            }
        }

        stage("push to docker hub") {
            steps {
                echo "This is pushing the image to docker hub"
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhubcred',
                    usernameVariable: 'dockerHubUser',
                    passwordVariable: 'dockerHubPass'
                )]) {
                    sh "docker login -u ${dockerHubUser} -p ${dockerHubPass}"
                    sh "docker image tag notes-app:latest sanskarwhizhack/notes-app:latest"
                    sh "docker push sanskarwhizhack/notes-app:latest"
                }
            }
        }

        stage("Deploy") {
            steps {
                echo "This is deploying a code"
                sh "docker-compose up -d"
            }
        }
    }
}

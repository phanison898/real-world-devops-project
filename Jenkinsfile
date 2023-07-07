pipeline {
    agent any

    stages {

        stage("Fetch Code") {
            steps {
                git url: "https://github.com/", branch: "master"
            }
        }

        stage('Build') {
            steps {
                script {
                    docker.build('express-server:latest', '.')
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    docker.image('express-server:latest').withRun { c ->
                        sh "docker run --name my-container -d ${c.id}"
                    }
                }
            }
        }
    }
}

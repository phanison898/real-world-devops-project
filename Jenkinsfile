pipeline {
    agent any

    stages {

        stage("Fetch Code") {
            steps {
                git url: "https://github.com/phanison898/real-world-devops-project.git", branch: "main"
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
                        sh "docker run -p 3000:3000 --name express-container -d ${c.id}"
                    }
                }
            }
        }
    }
}

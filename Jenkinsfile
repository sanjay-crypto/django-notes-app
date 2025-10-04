@Library("Shared") _
pipeline {
    agent { label "vinod" }

    stages {
        stage ("Code") {
            steps {
                script {
                    clone("https://github.com/sanjay-crypto/django-notes-app.git", "main")
                }
            }
        }
        stage ("Build") {
            steps {
                script {
                    docker_build("notes-app","latest","sanjayjadhav")
                }
            }
        }
        stage ("Push") {
            steps {
                echo "Push image to docker hub" 
                script {
                    docker_push("notes-app","latest", "sanjayjadhav")
                }
            }
        }
        stage ("Deploy") {
            steps {
                echo "Deploying the code"
                //sh "docker run -d -p 8000:8000 notes-app:latest"
                //sh "docker stop $(docker ps -aq)"
                //sh "docker rm -f $(docker ps -aq)"
                sh "docker compose down && docker compose up -d"
            }
        }
    }
}

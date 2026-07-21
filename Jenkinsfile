pipeline {
    agent { label "vinod" }

    stages {
        stage("Code") {
            steps {
                echo "This is cloning the code"
                git url: "https://github.com/Wizard991/django-notes-app.git", branch: "main"
            }
        }

        stage("Build") {
            steps {
                sh "docker build -t notes-app:latest ."
            }
        }

        stage("Push to DockerHub") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "dockerHubCred",
                    usernameVariable: "dockerHubUser",
                    passwordVariable: "dockerHubPass"
                )]) {
                    sh """
                    echo \$dockerHubPass | docker login -u \$dockerHubUser --password-stdin
                    docker tag notes-app:latest yash93344/notes-app:latest
                    docker push yash93344/notes-app:latest
                    """
                }
            }
        }

        stage("Deploy") {
            steps {
                sh '''
                    docker compose down
                    docker compose up -d --build
                '''
            }
        }
    }
}

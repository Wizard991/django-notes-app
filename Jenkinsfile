@Library('Shared') _

pipeline {
    agent { label "vinod" }

    stages {

        stage("Code") {
            steps {
                clone("https://github.com/Wizard991/django-notes-app.git", "main")
            }
        }

        stage("Build") {
            steps {
                dockerbuild("notes-app", "latest")
            }
        }

        stage("Push to DockerHub") {
            steps {
                dockerpush("dockerHubCred", "notes-app", "latest")
            }
        }

        stage("Deploy") {
            steps {
                deploy()
            }
        }
    }
}

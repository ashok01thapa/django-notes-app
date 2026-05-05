@Library("Shared") _
pipeline {
    
    agent { label "ash"}
    
    stages{
        
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        
        stage("Code"){
            steps{
                echo "This is cloning the code"
                script{
                clone("https://github.com/ashok01thapa/django-notes-app.git", "main")
                }
                echo "Code cloning successful"
            }
        }
        stage("Build"){
            steps{
                echo "This is building the code"
                script{
                docker_build("notes-app","latest","ashokthapa")
                }
            }
        }
        stage("Push to DockerHub"){
            steps{
                echo "This is pushing the image to Docker Hub"
              script{
                  docker_push("notes-app", "latest", "ashokthapa")
              }
            }
        }
        stage("Deploy"){
            steps{
                echo "This is deploying the code"
                sh "docker compose down && docker compose up -d"
            }
        }
    }
}

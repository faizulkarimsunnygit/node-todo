pipeline {
    agent any
    
    stages {
        
        stage("code"){
            steps{
                git url: "https://github.com/faizulkarimsunnygit/node-todo.git", branch: "main"
                echo 'Git Clone Complete'
            }
        }
        stage("build"){
            steps{
                sh "docker build -t node-app ."
                echo 'code build is done'
                sh 'docker tag node-app sunnyboysb/node-app:latest'
            }
        }

        stage("push"){
            steps{
                withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
                sh 'docker login -u sunnyboysb -p $PASSWORD'
                }
                sh 'docker push  sunnyboysb/node-app:latest'
                echo 'image push is done'
                }
            }
        }
        stage("deploy"){
            steps{
                sh 'kubectl apply -f deployment.yml'
                echo 'deployment done'
            }
        }
    }


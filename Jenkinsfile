pipeline {
    agent any
    
    stages{
        stage("clone code"){
            steps {
               echo "clone the code"
               git url:"https://github.com/sushovanmedda98/django-notes-app.git", branch: "main"
            }
        }
        stage("build"){
            steps {
                echo "build the code"
                sh "docker build . -t my-notes-app"
            }
        }
        stage("push the hub"){
            steps {
                echo "docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){
                sh "docker tag my-notes-app ${env.dockerhubUser}/my-notes-app:latest"
                sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
                sh "docker push ${env.dockerhubUser}/my-notes-app:v1"
                }
                
            }
        }
        stage("deploy"){
            steps {
                echo "deployed"
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
        
    }
}

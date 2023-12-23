pipeline{
    
    agent any
    
    stages{
        
        stage("code"){
            steps{
                echo "cloning the code"
                git url: "https://github.com/128844/django-notes-app", branch: "main"
            }
        }
        
        stage("build"){
            steps{
                echo "build the code"
                sh "docker build -t note-app ." 
            }
            
        }
        
        stage("push to docker hub"){
            steps{
                echo "pushing to docker hub."
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag note-app ${env.dockerHubUser}/note-app:one"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/note-app:one" 
                }
            }
            
        }
        
        stage("deploy"){
            steps{
                echo "deploy the container"
                sh "docker compose down && docker compose up -d"
                
                
            }
            
        }
    }
}

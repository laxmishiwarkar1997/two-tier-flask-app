@Library("Shared") _
pipeline{
    agent any;
    stages{
        stage("code"){
            steps{
                git url:"https://github.com/laxmishiwarkar1997/two-tier-flask-app.git", branch:"master"
                
            }
        }
         stage("Build"){
               steps{
                   
                sh "docker build -t my-two-tier-app ."
               }
         }
          stage("Test"){
                steps{echo "devloper test likkh k dega "}
          }
          stage("Push to dockerhub"){
                steps{
                    withCredentials([usernamePassword(
                    credentialsId:"dockerhubcreds",
                    passwordVariable:"dockerhubpass",
                    usernameVariable:"dockerhubuser"
                    )]){
                    sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
                    sh "docker image tag my-two-tier-app ${env.dockerhubuser}/my-two-tier-app"
                    sh "docker push ${env.dockerhubuser}/my-two-tier-app "
                    
                    }
                }
          }
           stage("deploy"){
               
                 steps{
                     
                     
                     sh "docker compose up -d --build flask-app"
                     
                 }
           }
    }
}

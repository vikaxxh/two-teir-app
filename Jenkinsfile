pipeline{
    
    agent any;
    
    stages{
        stage("Code"){
            steps{
                git url :"https://github.com/vikaxxh/two-teir-app.git", branch:"master"
                echo"Code clone ho gya"
            }
        }
        stage("Build"){
             steps{
                 sh "docker build -t flask-app ."
            }
        }
        stage("Test"){
             steps{
                echo"Testing bhi ho gyi"
            }
        }
        
        stage("push to docker hub"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerHubCreds', 
                                                 usernameVariable: 'DOCKER_USER', 
                                                 passwordVariable: 'DOCKER_PASS')]){
                sh "docker login -u ${env.DOCKER_USER} -p ${DOCKER_PASS}"
                sh "docker image tag flask-app ${env.DOCKER_USER}/two-tier-app "
                sh "docker push ${env.DOCKER_USER}/two-tier-app:latest"
            }
            }
        }
        stage("Deploy"){
             steps{
               sh "docker compose up -d --build flask-app"
            }
        }
    }
}

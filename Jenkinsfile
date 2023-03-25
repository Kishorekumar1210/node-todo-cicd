pipeline{
    agent { label'node-agent' }
    
    stages{
        stage('Code'){
            steps{
                git  url: 'https://github.com/Kishorekumar1210/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('Build'){
            steps{
                sh 'docker build . -t kishore1210/node-todo-test:latest'
            }
        }
        stage('Push'){
            steps{
               withCredentials([usernamePassword(credentialsId: 'DockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]){
                 sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                 sh 'docker push kishore1210/node-todo-test:latest'
                }
            }
        }
        stage('Test'){
            steps{
                echo "Testing the code"
            }
        }
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
        
        
        
    }
    
    
    
}

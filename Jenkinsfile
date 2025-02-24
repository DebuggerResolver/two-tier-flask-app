 pipeline {
    agent any

    stages {
        stage('code') {
            steps {
                git url:"https://github.com/DebuggerResolver/two-tier-flask-app.git" , branch :"master"
            }
        }
        stage('build'){
            steps{
                sh "docker build -t app ."
            }
        }
        stage("push to docker hub"){
            steps {
                withCredentials([usernamePassword(
                    credentialsId:"dockerHubCreds",
                    passwordVariable:"dockerHubPass",
                    usernameVariable: "dockerHubUser"
                    )]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag app ${env.dockerHubUser}/app"
                sh "docker push ${env.dockerHubUser}/app:latest"
                }
            }
        }
        stage('Test'){
            steps{
                sh "echo 'Code deploy ho. gaya' "
            }
        }
        stage('Deploy'){
            steps{
                sh "docker compose build"
            }
        }
    }
    
}

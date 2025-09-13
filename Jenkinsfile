pipeline{
    agent any
    
    stages{
        stage("Code Clone"){
            steps{
                echo "Code Clone Stage"
                git branch: 'master', url: 'https://github.com/Mayur4664/node-todo-cicd.git'
                }
        }
        stage("Code Build"){
            steps{
                echo "Code Build Stage"
                sh '/usr/local/bin/docker build . -t mayur010/node-todo-app:latest'
            }
        }
        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerHub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                sh 'docker push mayur010/node-todo-app:latest'
        }
    }
}
        stage("Deploy"){
            steps{
                sh "docker compose down && docker compose up -d"
            }
        }
     }
}


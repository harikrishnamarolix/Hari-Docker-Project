pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials ('dockerhub_id')
    }
    stages {
        stage('Git Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/harikrishnamarolix/Hari-Docker-Project.git'
            }
        }
        stage('Build Maven') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Build docker image') {
            steps {  
                sh 'docker build -t harimarolix/nodeapp:$BUILD_NUMBER .'
            }
        }
         stage('Run Container') {
            steps {  
                sh 'docker run -itd --name cont4 -p 8087:80 harimarolix/nodeapp:5'
            }
        }
        
         stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push harimarolix/nodeapp:$BUILD_NUMBER'
            }
        }
    }
}

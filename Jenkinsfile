pipeline {
    agent any

    stages {
        
        stage("Clone Code"){
            steps{
                echo 'Cloning the code from git.'
                git url : "https://github.com/Tarunashwini/django-notes-app.git", branch: "main"
            }
        }
        
        
        stage("Build Code"){
            steps{
                echo 'Building the code from git.'
                sh "docker build -t my-note-app ."
            }
        }
        
        
        stage('Pushing the docker file to the dockerhub') {
            steps {
                echo 'Pushing the image to docker hub'
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dpass", usernameVariable:"duser")]){
                    sh "docker tag my-note-app ${env.duser}/my-note-app"
                    sh "docker login -u ${env.duser} -p ${env.dpass}"
                    sh "docker push ${env.duser}/my-note-app:latest"
                    
                }
            }
        }
        
        stage("Runing the code"){
            steps{
                echo 'Running the code from git.'
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}

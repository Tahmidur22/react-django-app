pipeline {
    agent { label 'dev-agent' }
    stages {
        stage("Code") {
            steps {
                 echo "Code cloned"
                 git url: 'https://github.com/Tahmidur22/react-django-app.git', branch: 'master'
            }
        }
        stage("Build") {
            steps {
                 echo "Code build"
                 sh 'docker build . -t tahmid55/react-django-app:latest'
            }
        }
        stage("Login and Push Image") {
            steps {
                 echo "Loggin to docker hub and pushing image"
                 withCredentials([usernamePassword(credentialsId:'dockerHub', passwordVariable:'dockerHubPassword', usernameVariable:'dockerHubUsername')]) {
                    sh "docker login -u ${env.dockerHubUsername} -p ${env.dockerHubPassword}"
                     sh 'docker push tahmid55/react-django-app:latest'
                 }
            }
        }
        stage("Deploy") {
            steps {
                 echo "Code deployed"
            }
        }
    }
}

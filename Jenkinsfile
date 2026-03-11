pipeline{
    agent any
    stages{
        stage("Code"){
            steps{
                deleteDir()
                git branch: 'master',url: "https://github.com/ZubairSolanki/automate-flask-app-CI-CD.git"
                echo "Code Clone"
            }
        }
        
        stage("Docker-Clean"){
            steps{
                sh "docker compose down -v || true"
                sh "docker system prune -af || true"
                echo "Docker clean ho gya"
            }
        }
        
        stage("Build"){
            steps{
                sh "docker build  --no-cache -t myapp ."
                echo "buil ho gya"
            }
        }
        
        stage("Test"){
            steps{
                echo "test ho gya"
            }
        }
        
       stage("Push Docker Hub") {
    steps {
        withCredentials([usernamePassword(
            credentialsId: "dockerID",
            usernameVariable: "user",
            passwordVariable: "pass"
        )]) {

            sh "docker login -u $user -p $pass"
            sh "docker tag myapp:latest $user/myapp:latest"
            sh "docker push $user/myapp:latest"
        }

        echo "Docker image pushed successfully"
    }
}
        stage("Deploy"){
            steps{
                sh "docker compose up -d --build --force-recreate"
                    echo "deploy ho gya"
            }
        }
        
    }
}

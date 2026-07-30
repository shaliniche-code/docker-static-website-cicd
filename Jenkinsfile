pipeline {
    agent any 
        
        stages {
            
            stage("git checkout") {
                steps {
                git branch: 'main', 
                credentialsId: 'github-creds', 
                url: 'git@github.com:shaliniche-code/docker-static-website-cicd.git'
                
            }
        }
        
             stage("listing the files") {
                 steps {
                     sh 'ls'
                 }
             }
             
             stage("Build doccker image"){
                 steps {
                     sh 'docker rmi docker-static-website:latest || true'
                     sh 'docker build -t docker-static-website:latest .'
                 }
             }
             
             stage("Deploy the container") {
                 steps {
                     sh 'docker rm -f static-website || true'
                     sh 'docker run -d -p 9000:80 --name static-website docker-static-website:latest'
                 }
             }
             
             stage("Health check")  {
                 steps {
                     sh '''
                     echo "checking application health"
                     curl -f http://localhost:9000
                     echo "Application is healthy"
                     '''
                 }
             }
    }
}

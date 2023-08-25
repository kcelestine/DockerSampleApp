pipeline {
    agent any
 stages {
  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t nginxtest:latest .' 
                sh 'docker tag nginxtest khadijahthegreat/nginxtest:latest'
                sh 'docker tag nginxtest khadijahthegreat/nginxtest:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerlogin", url: "" ]) {
          sh  'docker push khadijahthegreat/nginxtest:latest'
          sh  'docker push khadijahthegreat/nginxtest:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps {
                sh "docker run -d -p 4030:80 khadijahthegreat/nginxtest"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 4001:80 khadijahthegreat/nginxtest"
 
            }
        }
    }
}

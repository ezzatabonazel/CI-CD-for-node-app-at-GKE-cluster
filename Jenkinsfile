pipeline {
    agent any
    stages {
            stage('ci') {
            steps {
                sh "docker build . -t ezzatabonazel7/demo-node"
                }
            }  
            stage('login') {
            steps {
                 withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')])
                 {
                    sh "docker login -u ${USERNAME} -p ${PASSWORD}"
                }  
             }
          }   
            stage('push') {
            steps {
                sh "docker push ezzatabonazel7/demo-node"
                }  
            }
            stage('cd') {
            steps {
                sh '''
                kubectl create -f namespace.yaml
                kubectl create  -f k8s/deployment.yaml
                kubectl create -f k8s/svc.yaml
                '''
            }
            
        }
    }
}  
  

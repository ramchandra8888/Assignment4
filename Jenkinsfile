

pipeline {
    agent any
    environment{
         DOCKER_CRED= credentials('Docker')
    }
        
    
   

    stages {
        stage('fetchh-data') {
            steps {
                git branch: 'main', url:'https://github.com/ramchandra8888/Assignment4.git'
                
            }
        }
        stage('build-image'){
            steps{
                sh 'docker build -t ramchandra123/assign4:${BUILD_NUMBER} .'
            }
        }
        stage('push-image'){
            steps{
                sh 'echo $DOCKER_CRED_PSW | docker login -u $DOCKER_CRED_USR --password-stdin'
                sh 'docker push ramchandra123/assign4:${BUILD_NUMBER}'
            }
        }
        stage("update-minikube"){
            steps{
                sh 'kubectl set image deployment/asn41 jenkins-app=ramchandra123/assign4:${BUILD_NUMBER}'
            }
            
        }
    }
}

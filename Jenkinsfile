pipeline {
    agent any
    tools{
        maven "Maven3"
    }
    stages{
        stage("Build Maven Project"){
            steps{
               checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Java-Techie-jt/devops-automation.git']]])
               sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t nilimaraut1994/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                      sh 'docker login -u rutujapawal -p ${dockerhubpwd}'
                      
                      sh 'docker push rutujapawal/devops-integration'
                    }    
                }
            }
        }
    }
}  
    

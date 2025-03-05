pipeline {
    agent any
    stages{
        stage('CodeScan'){
            steps{
                sh 'trivy --version'
                sh 'trivy fs . -o result.html'
                sh 'cat result.html'
            
    
            }
        }
        stage('dockerLogin'){
            steps{
                sh 'aws ecr get-login-password --region us-east-1 | \
                docker login --username AWS --password-stdin 890742578441.dkr.ecr.us-east-1.amazonaws.com'
            }
        }
        stage('dockerImageBuild'){
            steps{
                sh 'docker -v'
                sh 'docker build -t jenkins-ci .'
            }
        }
        stage('dockerImageTag'){
            steps{
                sh 'docker tag jenkins-ci:latest 890742578441.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci:latest'
                sh 'docker tag imageversion 890742578441.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci:v1.$BUILD_NUMBER'
            }
        }
        stage('pushImage'){
            steps{
                sh 'docker push 890742578441.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci:latest'
                sh 'docker push 890742578441.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci:v1.$BUILD_NUMBER'
            
            }
        }
    }

}
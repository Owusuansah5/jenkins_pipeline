pipeline {
    agent any
    stages{
        stage('CodeScan'){
            steps{
                sh 'trivy --version'
                sh 'trivy fs . -o result.html'
            
    
            }
        }
        stage('dockerImageBuild'){
            steps{
                sh 'docker -v'
            }
        }
        stage('pushImage'){
            steps{
                sh 'touch text-$BUILD_ID'
                sh 'docker ps'
            }
        }
    }

}
pipeline{
    agent any

    stages {

        stage('Checkout Code') {

            steps {
                
                script {
                    
                    git branch: 'main', url: 'https://github.com/MuhammadAhsanDonuts/devops_proj_1.git'
                }
                
            }
        }

        stage('Unit Testing') {

            steps {

                 script {
                    
                    sh 'mvn test'
                }
                 
            }
        }

        stage('Integration Testing') {

            steps {

                 script {
                    
                    sh 'mvn verify -DskipUnitTests'
                }
                 
            }
        }

        stage('Maven build'){
            
            steps{
                
                script{
                    
                    sh 'mvn clean install'
                }
            }
        }
        
        stage('Static code analysis'){
            
            steps{
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'SONARQUBE-API') {
                        
                        sh 'mvn clean package sonar:sonar'

                    }
                }
                    
            }
        }
    }

}

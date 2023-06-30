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

        stage('Quality Gate Status'){
                
            steps{
                    
                script{
                        
                        waitForQualityGate abortPipeline: false, credentialsId: 'SONARQUBE-API'
                }
            }
        }

        stage('Nexus Artifact Upload'){
                
            steps{
                    
                script{
                    
                       nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: '', file: 'target/Uber.jar', type: 'jar']], credentialsId: 'NEXUS_API', groupId: 'com.example', nexusUrl: '172.173.226.41:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'demo-app-springboot', version: "1.0.1"
                }
            }
        }

    }

}

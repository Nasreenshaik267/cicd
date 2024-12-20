pipeline {
    agent any
    
    tools {
        maven 'maven3'
        jdk 'jdk17'
    }

    environment {

        SCANNER_HOME = tool 'sonar-scanner'
    }
    
        stages {
          
         stage('Git CheckOut') {
            steps {
                git branch: 'main' , url: 'https://github.com/Nasreenshaik267/cicd.git'
             }
          }

        stage('Versioning') {
            steps {
                script{
                sh 'mvn versions:set -DnewVersion=1.0.${BUILD_NUMBER}'
                }
            }
        }

        stage('Maven Compile') {
            steps {
               echo 'Maven Compile Started'
               sh 'mvn compile'
            }
        } 

        stage('Maven Test') {
            steps {
               echo 'Maven Test Started'
               sh 'mvn test'
            }
        }
        
        stage('Sonar Analysis') {
            steps {
               withSonarQubeEnv(credentialsId: 'sonarqube-token', installationName: 'SonarQube') {
                sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=SpringBootApp -Dsonar.projectKey=SpringBootApp \
                                                       -Dsonar.java.binaries=. -Dsonar.exclusions=/trivy-fs-output.txt '''
               }
            }
        } 

        stage('qualitygate') {
            steps {
               script{
                
                waitForQualityGate abortPipeline: false, credentialsId:'sonarqube-token'
                
               }
            }

        }
        
        stage('File System Scan by Trivy') {
            steps {
               echo 'Trivy Scan Started'
               sh 'trivy fs --format table --output trivy-fs-output.txt .'
            }
        } 
        
    }

}
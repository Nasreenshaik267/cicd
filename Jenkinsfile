
pipeline {
    agent any
    tools {
        maven 'maven3'
        jdk 'jdk17'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main' , url: 'https://github.com/Nasreenshaik267/cicd.git'
            }
        }
        stage('Versioning') {
            steps {
                script {
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
    }
}      
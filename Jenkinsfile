
pipeline {
    agent any
    tools {
        maven 'maven3'
        jdk 'jdk17'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'prod' , url: 'https://github.com/bkrrajmali/aws-cicd-evening.git'
            }
        }
    }
}      
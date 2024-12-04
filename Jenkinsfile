
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
    }
}      
pipeline {
    agent any
    
    tools {
        maven 'maven-3.8.5'
    }
    
    stages {
        stage('cod checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/zielotech-batc/standalone-app.git'
            }
        }
        
        stage('mvn build') {
            steps {
                sh 'mvn -v'
                sh 'mvn clean package'
            }
        }
    }
} 

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
            post {
                success {
                    archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
                }
            }
        }
        stage('static analusis') {
            steps {
                sh 'mvn checkstyle:checkstyle pmd:pmd'
                recordIssues(tools: [checkStyle(pattern: '**/checkstyle-result.xml')])
                recordIssues(tools: [pmdParser(pattern: '**/pmd.xml')])
            }
        }
        stage('code coverage') {
            steps {
                jacoco maximumBranchCoverage: '80', maximumClassCoverage: '80', maximumComplexityCoverage: '80', maximumInstructionCoverage: '80', maximumLineCoverage: '80', maximumMethodCoverage: '80', minimumBranchCoverage: '80', minimumClassCoverage: '80', minimumComplexityCoverage: '80', minimumInstructionCoverage: '80', minimumLineCoverage: '80', minimumMethodCoverage: '80'
            }
        }
        stage('build & publish') {
            steps {
                sh '''
                      docker build -t jar-image .
                      docker tag jar-image:latest  jadhavshubham/webapp-zeilotech:v4
                      docker push jadhavshubham/webapp-zeilotech:v4
                '''
            }
        }
        stage('ECHO'){
            parallel{
                stage('stage1'){
                    steps {
                        echo "india"
                    }
                }
                stage('stage2'){
                    steps{
                        echo "pakistan"
                    }
                }
            }
        }
    }
}

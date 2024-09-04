pipeline {
    agent any

    tools {
        jdk 'jdk11'
        maven 'maven3'
    }
    
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    
    stages {
        stage('Git checkout') {
            steps {
                git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/AbsoluteZero24/sonar-analysis-springboot.git'
            }
        }
    
        stage('compile code') {
            steps {
                sh "mvn clean compile"
            }
        }

        stage('code test') {
            steps {
                sh "mvn test"
            }
        }
        
        stage('sonar analsys') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=sonar-qube-analsys \
                    -Dsonar.java.binaries=. \
                    -Dsonar.projectKey=sonar-qube-analsys '''
                }
            }
        }
    }
}

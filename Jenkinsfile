pipeline {
    agent any

    tools {
        maven 'Maven3'  // Must match Maven tool name in Jenkins
        hudson.plugins.sonar.SonarRunnerInstallation 'SonarScanner' // Must match SonarScanner tool name in Jenkins
    }

    environment {
        SONARQUBE_SERVER = 'SonarQubeServer'  // SonarQube server name in Jenkins config
        SONAR_TOKEN = 'sqa_d9191259bdb43236dee6e9185337370af28c6ec8'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/ADirin/Week4_Inclass_Assignment_SonarQube_Jenkins.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQubeServer') {
                    bat """
                        ${tool 'SonarScanner'}\\bin\\sonar-scanner ^
                        -Dsonar.projectKey=devops-demo ^
                        -Dsonar.sources=src ^
                        -Dsonar.projectName=DevOps-Demo ^
                        -Dsonar.host.url=http://localhost:9000 ^
                        -Dsonar.login=${env.SONAR_TOKEN} ^
                        -Dsonar.java.binaries=target/classes
                    """
                }
            }
        }
    }
}
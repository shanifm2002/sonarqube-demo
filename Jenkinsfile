pipeline {
    agent any

    tools {
        // Ensure 'maven-3.9' is the exact name in Global Tool Configuration
        maven 'maven' 
    }

    environment {
        // Ensure 'SonarScanner' is the exact name in Global Tool Configuration
        SONAR_SCANNER_HOME = tool 'SonarScanner' 
    }

    stages {
        stage('Checkout Code') {
            steps {
                // *** FIX: Explicitly specify the branch ***
                git branch: 'main', 
                    url: 'https://github.com/Irfaanpk/sonarqube-demo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Ensure 'SonarQube' matches the server name in Jenkins config
                withSonarQubeEnv('SonarQube') { 
                    sh '''
                    # Using the Maven sonar plugin for analysis
                    mvn sonar:sonar \
                    -Dsonar.projectKey=java-demo
                    '''
                }
            }
        }
    }
}

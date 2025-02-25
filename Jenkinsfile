pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ahmedbenameur/my_application.git'
                sh 'ls -l'  // Print workspace contents
            }
        }
        stage('Scan') {
            steps {
                withSonarQubeEnv(installationName: 'sq1') { 
                    sh 'ls -l'  // Check if pom.xml exists
                    sh 'mvn clean org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar'
                }
            }
        }
    }
}

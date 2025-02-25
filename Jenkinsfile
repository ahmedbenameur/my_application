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

        stage('Check') {
            steps {
               sh ' python3 script.py '
            }
        }
        
        stage('Scan') {
            steps {
                withSonarQubeEnv(installationName: 'sq1') {
                    // Run SonarScanner on the extracted Java files
                    script {
                       

                        sh """
                        sonar-scanner \
                        -Dsonar.projectKey=application \
                        -Dsonar.sources=extracted_code/java \
                        -Dsonar.host.url=http://localhost:9000/ \
                     
                        """
                }
            }
        }
    }
}

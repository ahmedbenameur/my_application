pipeline {
    agent any
    stages {
        stage('Install SonarQube Scanner') {
            steps {
                script {
                    // Install sonar-scanner if not already installed
                    sh '''
                    
                       
                      
                       
                        ln -s /var/jenkins_home/sonar-scanner/sonar-scanner-4.6.2.2472-linux/bin/sonar-scanner /usr/local/bin/sonar-scanner
                    else
                        echo "SonarQube Scanner already installed"
                    fi
                    '''
                }
            }
        }
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ahmedbenameur/my_application.git'
            }
        }
        stage('Scan') {
            steps {
                withSonarQubeEnv(installationName: 'sq1') {
                    script {
                        // Run SonarScanner
                        sh '''
                        sonar-scanner \
                        -Dsonar.projectKey=application \
                        -Dsonar.sources=extracted_code/java \
                        -Dsonar.host.url=http://localhost:9000/
                        '''
                    }
                }
            }
        }
    }
}

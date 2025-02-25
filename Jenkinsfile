pipeline {
    agent any
    stages {
        stage('Install SonarQube Scanner') {
            steps {
                script {
                    // Install sonar-scanner with elevated privileges
                    sh '''
                    if ! command -v sonar-scanner &>/dev/null; then
                        echo "SonarQube Scanner not found, installing..."
                        wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.6.2.2472-linux.zip
                        unzip sonar-scanner-cli-4.6.2.2472-linux.zip
                         // Example of a custom installation directory
                        sh 'mkdir -p /var/jenkins_home/sonar-scanner'
                        sh 'mv sonar-scanner-4.6.2.2472-linux /var/jenkins_home/sonar-scanner'
                       
                        sudo ln -s /opt/sonar-scanner/bin/sonar-scanner /usr/local/bin/sonar-scanner
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

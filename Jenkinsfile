pipeline {
    agent any
    stages {
        stage('Install SonarQube Scanner') {
            steps {
                script {
                    // Install sonar-scanner if not already installed
                    sh '''
                    if ! command -v sonar-scanner &>/dev/null; then
                        echo "SonarQube Scanner not found, installing..."
                        wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.6.2.2472-linux.zip
                        unzip -o sonar-scanner-cli-4.6.2.2472-linux.zip

                        // Custom installation directory
                        mkdir -p /var/jenkins_home/sonar-scanner
                        mv sonar-scanner-4.6.2.2472-linux /var/jenkins_home/sonar-scanner
                       
                        sudo ln -s /var/jenkins_home/sonar-scanner/sonar-scanner-4.6.2.2472-linux/bin/sonar-scanner /usr/local/bin/sonar-scanner
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

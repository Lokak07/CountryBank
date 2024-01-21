pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/jaiswaladi246/CountryBank.git'
            }
        }
        
        stage('OWASP Dependency Check') {
            steps {
                script {
                    dependencyCheck additionalArguments: ' --scan ./ ', odcInstallation: 'DC'
                    dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
                }
            }
        }
        
        stage('Build & deploy') {
            steps {
                script {
                    // Execute the Docker Compose command
                    sh 'docker-compose up -d'
                }
            }
        }
    }
}

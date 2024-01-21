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
        
        stage('Install Docker Compose') {
    steps {
        script {
            sh 'sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose'
            sh 'sudo chmod +x /usr/local/bin/docker-compose'
        }
    }
}


        stage('Verify Docker Compose Installation') {
            steps {
        script {
            sh 'docker-compose --version'
        }
    }
}


        stage('Build & deploy') {
            steps {
                script {
                    // Load and execute the Jenkinsfile from another repository
                    load 'docker-compose up -d'
                }
            }
        }
    }
}

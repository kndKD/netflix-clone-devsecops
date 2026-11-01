pipeline {
    agent any 

    tools {
        nodejs 'NodeJS' 
    }

    stages {
        stage('1. Checkout Code') {
            steps {
                echo 'Checking out code from GitHub...'
                checkout scm
            }
        }
        
        stage('2. Build App') {
            steps {
                echo 'Building React App...'
                sh 'npm install'
                sh 'npm run build'
            }
        }
        
        stage('3. Build Docker Image') {
            steps {
                echo 'Building Docker Image...'
                sh 'docker build -t netflix-clone-devsecops:latest .'
            }
        }

        stage('4. Trivy Security Scan') {
            steps {
                echo 'Running Trivy Security Scan on Docker Image...'
                sh 'docker run --rm -v /var/run/docker.sock:/var/run/docker.sock aquasec/trivy:latest image --severity CRITICAL,HIGH --exit-code 1 netflix-clone-devsecops:latest'
            }
        }
    }
    
    post {
        success {
            echo '✅ Build and Security Scan Successful!'
        }
        failure {
            echo '❌ Pipeline Failed. Please check the Console Output.'
        }
    }
}
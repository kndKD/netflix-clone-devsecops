pipeline {
    agent any 

    tools {
        
        nodejs 'NodeJS' 
    }

    stages {
        stage('1. Checkout Code') {
            steps {
                echo 'GitHub pull code'
                checkout scm
            }
        }
        
        stage('2. Build App') {
            steps {
                echo 'React App  Dependencies install '
                sh 'npm install'
                echo 'React App build '
                sh 'npm run build'
            }
        }
    }
    
    post {
        success {
            echo '✅ Build  successful '
        }
        failure {
            echo '❌ Build  unsuccessful '
        }
    }
}
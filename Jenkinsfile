pipeline {
    agent any

    environment {
        NODE_ENV = 'production'
    }

    stages {
        stage('Checkout') {
            steps {
                echo '📥 Cloning repository...'
                git 'https://github.com/janpatmat/JenkinsSBPipeline.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo '📦 Installing dependencies...'
                sh 'npm ci'
            }
        }

        stage('Build') {
            steps {
                echo '🏗️ Building the React app...'
                sh 'npm run build'
            }
        }

        stage('Deploy to Host') {
            steps {
                echo '🚀 Deploying to host web server...'
                // Replace /var/www/html with your actual deploy target path
                sh '''
                    rm -rf /var/www/html/*
                    cp -r build/* /var/www/html/
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Build and deployment successful!'
        }
        failure {
            echo '❌ Something went wrong!'
        }
    }
}

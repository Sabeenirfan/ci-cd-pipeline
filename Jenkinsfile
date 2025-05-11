pipeline {
    agent any

    environment {
        PROJECT_NAME = 'construction'
        GITHUB_URL = 'https://github.com/Sabeenirfan/ci-cd-pipeline.git'
    }

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'GitHub-PAT', url: "${GITHUB_URL}", branch: 'main'
            }
        }

        stage('Build') {
            steps {
                bat 'docker-compose -f docker-compose.yml down || exit 0'
                bat "docker-compose -p %PROJECT_NAME% -f docker-compose.yml up -d --build"
            }
        }

        stage('Test') {
            steps {
                echo 'Testing the application...'
                // You can add: bat "docker exec container-name npm test"
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
            }
        }
    }

    post {
        success {
            echo '✅ Build completed successfully.'
        }
        failure {
            echo '❌ Build failed.'
        }
    }
}

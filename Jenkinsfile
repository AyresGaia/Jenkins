pipeline {
    agent any

    tools {
        nodejs "NodeJS_18" // Jenkins NodeJS tool
    }

    environment {
        VERCEL_TOKEN = credentials('Zm0ANbNe40kXb6lmox9melJf')
        VERCEL_PROJECT = 'Jenkins-Ci-Cd'
        VERCEL_ORG = 'team_qUDl7zDRO52W0KtfATbSaR5n'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/AyresGaia/Jenkins-Ci-Cd.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Deploy to Vercel') {
            steps {
                sh """
                npx vercel --token $VERCEL_TOKEN --prod --confirm
                """
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful 🚀'
        }
        failure {
            echo 'Pipeline Failed ❌'
        }
    }
}

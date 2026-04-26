pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    environment {
        REPO_URL = 'https://github.com/Shreya-Rajashekara12/demo12.git'
        BRANCH = 'main'
    }

    stages {

        stage('CHECKOUT') {
            steps {
                git branch: "${BRANCH}", url: "${REPO_URL}"
            }
        }

        stage('BUILD') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('TEST') {
            steps {
                bat 'mvn test'
            }
        }
    }

    post {
        success {
            echo 'Build Successful ✅'

            // Slack Notification
            slackSend channel: '#jenkins', message: "SUCCESS: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' completed."

            // Email Notification
            emailext(
                to: 'your-email@gmail.com',
                subject: "SUCCESS: ${env.JOB_NAME} Build #${env.BUILD_NUMBER}",
                body: "Build completed successfully.\nCheck console output at ${env.BUILD_URL}"
            )
        }

        failure {
            echo 'Build Failed ❌'

            // Slack Notification
            slackSend channel: '#jenkins', message: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' failed."

            // Email Notification
            emailext(
                to: 'your-email@gmail.com',
                subject: "FAILED: ${env.JOB_NAME} Build #${env.BUILD_NUMBER}",
                body: "Build failed.\nCheck console output at ${env.BUILD_URL}"
            )
        }
    }
}

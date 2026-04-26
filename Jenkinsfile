pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {

        stage('CHECKOUT') {
            steps {
                git branch: 'main', url: 'https://github.com/Shreya-Rajashekara12/demo12.git'
            }
        }

        stage('BUILD') {
            steps {
                bat 'dir'   // DEBUG: shows files
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
        }
        failure {
            echo 'Build Failed ❌'
        }
    }
}

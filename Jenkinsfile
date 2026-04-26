pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/Shreya-Rajashekara12/demo12.git'
            }
        }

        stage('Build') {
            steps {
                dir('demo12') {
                    bat 'mvn clean install'
                }
            }
        }

        stage('Test') {
            steps {
                dir('demo12') {
                    bat 'mvn test'
                }
            }
        }
    }
}

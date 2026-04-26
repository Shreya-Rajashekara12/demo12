pipeline {
    agent any

    tools {
        // Must match name in Manage Jenkins -> Global Tool Configuration
        maven 'Maven3'
    }

    stages {
        stage('CHECKOUT') {
            steps {
                // Clones the repo into the workspace
                git branch: 'main', url: 'https://github.com/Shreya-Rajashekara12/demo12.git'
            }
        }

        stage('BUILD') {
            steps {
                // Switch to the 'demo12' subfolder to find pom.xml
                dir('demo12') {
                    echo 'Building from the demo12 subfolder...'
                    // -DskipTests avoids running tests twice (we do them in the next stage)
                    bat 'mvn clean install -DskipTests'
                }
            }
        }

        stage('TEST') {
            steps {
                dir('demo12') {
                    echo 'Running Tests...'
                    bat 'mvn test'
                }
            }
        }
    }

    post {
        always {
            // Records the test results in the Jenkins UI
            dir('demo12') {
                junit '**/target/surefire-reports/*.xml'
            }
        }
        success {
            echo 'Build Successful ✅'
            // Captures the JAR file so you can download it from the Jenkins build page
            archiveArtifacts artifacts: 'demo12/target/*.jar', fingerprint: true
        }
        failure {
            echo 'Build Failed ❌'
        }
    }
}

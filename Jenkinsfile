pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/BlairSlenders/DevOpsServerPipeline.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh 'echo Building the project...'
            }
        }

        stage('Test') {
            steps {
                sh 'echo Running tests...'
            }
        }
    }

    post {
        success {
            echo 'Build and tests completed successfully!'
        }
        failure {
            echo 'Build or tests failed.'
        }
    }
}

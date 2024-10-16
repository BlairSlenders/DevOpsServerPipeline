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
    
        stage('Deploy to Azure') {
            steps {
                script {
                    def resourceGroup = 'DeploymentWebApp_group'
                    def webAppName = 'DeploymentWebApp'
                    
                    sh """
                    echo 'Logging into Azure...'
                    az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET --tenant $AZURE_TENANT_ID
                    echo 'Deploying to Azure Web App...'
                    az webapp deployment source config-zip \
                      --resource-group ${resourceGroup} \
                      --name ${webAppName} \
                      --src-path target/deployable.zip
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Build, tests, and deployment completed successfully!'
        }
        failure {
            echo 'Build, tests, or deployment failed.'
        }
    }
}

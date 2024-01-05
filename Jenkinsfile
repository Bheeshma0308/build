pipeline
{
    agent any
    environment {
        MAVEN_GOALS = 'clean install'        // Define the Maven goals for building the project   
        AZURE_WEBAPP_NAME = 'mybuildappbheeshma'
        AZURE_RESOURCE_GROUP = 'mybuildappbheeshm_group'
        AZURE_PLAN_NAME = 'ASP-mybuildappbheeshmgroup-be30'
    }
    stages
    {
        stage('Checkout') 
        {
            steps
            {
                // Checkout the Git repository
                checkout([$class:'GitSCM',branches:[[name: '*/master']],doGenerateSubmoduleConfigurations:false,userRemoteConfigs:[[url:'https://github.com/Bheeshma0308/build.git']]])
            }
        }
        stage('Build')
        {
            steps
            {
                 script {
                 sh "mvn ${MAVEN_GOALS}"
                def jarFilePath = sh(script: 'find target -name "*.jar" | head -n 1', returnStdout: true).trim()
                 env.JAR_FILE_PATH = jarFilePath
                 }
            }
        }
    stage('Deploy to Azure') {
            steps {
                script {
                    // Authenticate with Azure CLI (make sure you've configured Azure CLI credentials in Jenkins)
                    sh 'az login'

                    // Deploy the Java application to Azure App Service
                    sh "az webapp deploy -g ${AZURE_RESOURCE_GROUP} -n ${AZURE_WEBAPP_NAME} --type jar --src ${env.JAR_FILE_PATH}"

                    // Optional: Restart the Azure App Service to apply changes
                    sh "az webapp restart -g ${AZURE_RESOURCE_GROUP} -n ${AZURE_WEBAPP_NAME}"
                }
            }
        }
    }
    post
    {
        success
        {
            echo "Build successful!"
        }
        failure 
        {
            echo "Build failed!"
        }
    }
}

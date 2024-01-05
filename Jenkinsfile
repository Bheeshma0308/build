pipeline
{
    agent any
    environment 
    {
        MAVEN_GOALS = 'clean install'        // Define the Maven goals for building the project  
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
                 sh "mvn ${MAVEN_GOALS}"
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

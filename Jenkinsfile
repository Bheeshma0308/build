pipeline
{
    agent any
    environment
    {
        GIT_REPO_URL ='https://github.com/Bheeshma0308/build.git'     // Define the Git repository URL
        MAVEN_GOALS = 'clean install'                                 // Define the Maven goals for building the project 
        PROJECT_DIR = 'your-java-project'                             // Define the project directory 
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
                // Change to the project directory
                dir(PROJECT_DIR)
                {
                    // Run Maven build
                    sh "mvn ${MAVEN_GOALS}"
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

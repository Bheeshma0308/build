pipeline {
    agent any
    def gitRepoUrl = 'https://github.com/Bheeshma0308/build.git'     // Define the Git repository URL
    def gitBranch = 'master'                                         // Define the branch to build
    def mavenGoals = 'clean install'                     // Define the Maven goals to build the Java application             
    stages {
        stage('Checkout') {
            steps {
                // Checkout the Git repository using SSH key credentials
                checkout([$class: 'GitSCM', 
                          branches: [[name: master]], 
                          userRemoteConfigs: [[url: https://github.com/Bheeshma0308/build.git ]],
                          extensions: [[$class: 'CheckoutOption', timeout: 60], [$class: 'CloneOption', sshUserPrivateKey: [credentialsId: 'your-ssh-credentials-id']]]])
            }
        }

        stage('Build') {
            steps {
                // Build the Java application using Maven
                script {
                    def mvnHome = tool 'Maven'
                    sh "${mvnHome}/bin/mvn ${mavenGoals}"
                }
            }
        }

        // Add additional stages for testing, deployment, etc.
            
        stage('Archive Artifacts') {
            steps {
                // Archive the built artifacts (e.g., JAR file)
                archiveArtifacts 'target/*.jar'
            }
        }
    }
    
    post {
        success {
            // Additional actions on build success
            echo 'Build successful! Deploy or perform other actions here.'
        }
        failure {
            // Additional actions on build failure
            echo 'Build failed! Handle failures or notify stakeholders here.'
        }
    }
}

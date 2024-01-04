pipeline {
    agent any
 
    stages {
        stage('checkout') {
            steps {
                // Clean workspace before cloning (optional)
                deleteDir()
                
                // Git checkout
checkout([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[url: 'https://github.com/Bheeshma0308/build.git']]])
            }
        }
 
        stage('Build') {
            steps {
                // Your build commands (Maven, Gradle, etc.)
                sh 'mvn clean install'
            }
        }
    }
}

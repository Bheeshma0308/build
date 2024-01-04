pipeline {
    agent any
 
    stages {
        stage('Clone Repository') {
            steps {
                // Clean workspace before cloning (optional)
                deleteDir()
                
                // Git checkout
checkout([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[url: ]]])
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

pipeline {
    
    agent any
    
    stages {
        
        stage('Checkout') {
            
            steps {
                
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[url: 'https://github.com/Bheeshma0308/build.git']]]) // Git checkout
            }
        }
 
        stage('Build') {
            steps {

                sh 'mvn clean install'          // Your build commands              
            }
        }
    }
}

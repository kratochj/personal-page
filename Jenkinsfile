pipeline {
    
    environment {
        registry = "registry.kratochvil.eu/personal-page"
        dockerImage = ‘’
    }
    
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }        
            }
        }
        stage('Push to registry') {
            steps{
                script {
                    docker.withRegistry( '' ) {
                        dockerImage.push()
                    }
                }
            }
        }   
    
    }
   
}

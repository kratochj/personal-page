pipeline {
    
    environment {
        registry = "registry.kratochvil.eu/personal-page"
        dockerImage = ''
    }
    
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build registry
                }        
            }
        }
        stage('Push to registry') {
            steps{
                script {
                    docker.withRegistry( '' ) {
                        dockerImage.push("$BUILD_NUMBER")
                        dockerImage.push("$GIT_COMMIT")
                        dockerImage.push("latest") 
                    }
                }
            }
        }   
    
    }
   
}

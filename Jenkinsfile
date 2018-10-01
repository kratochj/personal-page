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
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    dockerImage.tag "$GIT_COMMIT"
                }        
            }
        }
        stage('Push to registry') {
            steps{
                script {
                    docker.withRegistry( registry ) {
                        push()
                    }
                }
            }
        }   
    
    }
   
}

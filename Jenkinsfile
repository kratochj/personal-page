pipeline {
    
    environment {
       registry = "registry.kratochvil.eu/personal-page"
    }
    
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    docker.build registry + ":$BUILD_NUMBER"
                }        
            }
        }
    }
    stage(‘Push Image to registry’) {
        steps{
            script {
                docker.withRegistry( ‘’ ) {
                    dockerImage.push()
                }
            }
        }
    }
}

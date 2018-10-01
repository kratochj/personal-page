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
}

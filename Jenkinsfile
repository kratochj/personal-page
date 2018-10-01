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
		
		stage('Deploy to registry (master)') {
			when {
				 expression { env.BRANCH_NAME == "master" }
			}
			steps {
                script {
                    docker.withRegistry( '' ) {
                        dockerImage.push("$BUILD_NUMBER")
                        dockerImage.push("latest") 
                    }
                }
			}
		}
		
        stage('Deploy to registry (all)') {
            steps{
                script {
                    docker.withRegistry( '' ) {
                        dockerImage.push("$BRANCH_NAME-$BUILD_NUMBER")
                        dockerImage.push("$GIT_COMMIT")
                    }
                }
            }
        }   
    
    }
   
}

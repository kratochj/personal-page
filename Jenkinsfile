pipeline {
    
    environment {
        registry = "registry.kratochvil.eu/personal-page"
        dockerImage = ''
    }
    
    agent docker

    stages {
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build registry
                }        
            }
        }
		
        stage('Deploy to registry (all)') {
            steps{
            	script {
					echo "Deploying everything"
				}
                script {
                    docker.withRegistry( '' ) {
                        dockerImage.push("$BRANCH_NAME-$BUILD_NUMBER")
                        dockerImage.push("$GIT_COMMIT")
                    }
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
		stage('Redeploy image') {
			when {
				 expression { env.BRANCH_NAME == "master" }
			}
			steps {
            	script {
					echo "Deploying new docker image"
				}
                script {
						docker rm -f personal-page
                }
                script {
						docker run -d -p 27033:80 registry:$GIT_COMMIT
                }
			}
		}
    }
   
}

pipeline {
    
    environment {
        registry = "registry.kratochvil.eu/personal-page"
        dockerImage = ''
        registryCredential = 'dockerhub'
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
		
        stage('Deploy to registry (all)') {
            steps{
            	script {
					echo "Deploying everything"
				}
                script {
                    docker.withRegistry( 'https://registry.kratochvil.eu', registryCredential ) {
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
					echo "Deploying master"
				}
                script {
                    docker.withRegistry( 'https://registry.kratochvil.eu', registryCredential ) {
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
					echo "Deploying new docker image"
					sh "docker stop  personal-page"
					sh "docker rm personal-page"
					sh "docker run -d -p 27033:80 --name personal-page $registry:$GIT_COMMIT"
			}
		}
    }
   
}

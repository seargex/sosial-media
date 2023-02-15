pipeline {
    agent any
     environment {     
        DOCKERHUBLULU_CREDENTIALS= credentials('dockerhublulu')
        DOCKERHUBTIKA_CREDENTIALS= credentials('dockerhubtika')
        DOCKERHUBARDI_CREDENTIALS= credentials('dockerhubardi')
        LINUX_CREDENTIALS= credentials('linux')
    }
    stages {
        stage("Git Checkout"){  
            steps{     
	            git credentialsId: 'github', url: 'https://github.com/seargex/sosial-media'
	            echo 'Git Checkout Completed'   
            }
        }
        stage('Build Docker Image Lulu'){         
            steps{                
	            sh 'echo $LINUX_CREDENTIALS_PSW | sudo -S docker build -t lulufajar890/sosmed:${BUILD_NUMBER} .'
                echo 'Build Image Completed'                
            }
        }
        stage('Build Docker Image Tika'){         
            steps{                
	            sh 'echo $LINUX_CREDENTIALS_PSW | sudo -S docker build -t kartikaaaaaa/sosmed:${BUILD_NUMBER} .'
                echo 'Build Image Completed'                
            }
        }
        stage('Build Docker Image Ardi'){         
            steps{                
	            sh 'echo $LINUX_CREDENTIALS_PSW | sudo -S docker build -t seargex/sosmed:${BUILD_NUMBER} .'
                echo 'Build Image Completed'                
            }
        }
        stage('Login to Docker Hub Lulu'){         
            steps{                            
	            sh 'echo $DOCKERHUBLULU_CREDENTIALS_PSW | docker login -u lulufajar890 --password-stdin'
	            echo 'Login Completed'                
            }           
        }
        stage('Push Image to Docker Hub Lulu'){         
            steps{                            
	            sh 'docker push lulufajar890/sosmed:${BUILD_NUMBER}'
	            echo 'Push Image Completed'       
            }           
        }
        stage('Logout Docker Hub Lulu'){         
            steps{
                sh 'docker logout'
                echo 'Logout Completed'
            }           
        }
        stage('Login to Docker Hub Tika'){         
            steps{                            
	            sh 'echo $DOCKERHUBTIKA_CREDENTIALS_PSW | docker login -u kartikaaaaaa --password-stdin'
	            echo 'Login Completed'                
            }           
        }
        stage('Push Image to Docker Hub Tika'){         
            steps{                            
	            sh 'docker push kartikaaaaaa/sosmed:${BUILD_NUMBER}'
	            echo 'Push Image Completed'       
            }           
        }
        stage('Logout Docker Hub Tika'){         
            steps{
                sh 'docker logout'
                echo 'Logout Completed'
            }           
        }
        stage('Login to Docker Hub Ardi'){         
            steps{                            
	            sh 'echo $DOCKERHUBARDI_CREDENTIALS_PSW | docker login -u seargex --password-stdin'
	            echo 'Login Completed'                
            }           
        }
        stage('Push Image to Docker Hub Ardi'){         
            steps{                            
	            sh 'docker push seargex/sosmed:${BUILD_NUMBER}'
	            echo 'Push Image Completed'       
            }           
        }
        stage('Deploy CFmap to K8s'){
		    steps{
			    sh "envsubst < ${WORKSPACE}/manifest/pesbuk-cfmap.yml | kubectl apply -f -"
			    echo 'Deployment Completed'
		    }
        }
        stage('Deploy Secret to K8s'){
		    steps{
			    sh "envsubst < ${WORKSPACE}/manifest/pesbuk-secret.yml | kubectl apply -f -"
			    echo 'Deployment Completed'
		    }
        }
        stage('Deploy Svc to K8s'){
		    steps{
			    sh "envsubst < ${WORKSPACE}/manifest/pesbuk-svc.yml | kubectl apply -f -"
			    echo 'Deployment Completed'
		    }
        }
        stage('Deploy Pesbuk to K8s'){
		    steps{
			    sh "envsubst < ${WORKSPACE}/manifest/pesbuk-deploy.yml | kubectl apply -f -"
			    echo 'Deployment Completed'
		    }
        }
        stage('Logout Docker Hub Ardi'){         
            steps{
                sh 'docker logout'
                echo 'Logout Completed'
            }           
        }
    }
}
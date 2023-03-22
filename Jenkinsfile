pipeline {
    agent any
    
    environment {
		DOCKERHUB_CREDENTIALS=credentials('1beb4e63-e8f0-4b6c-9d91-48e1ac29b7ed')
	}
 
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'main', url: 'https://github.com/BhushanShete/JavaWebApp.git'
             
          }
        }
  stage('Maven Build') {
           steps {
             
                sh 'mvn --version'             
          }
      
         post {
                success {
                    archiveArtifacts artifacts: '**', followSymlinks: false
                }
            }
        }
  stage('Maven Test') {
           steps {
             
                sh 'test mvn'             
          }
        }
     stage('Build Docker Image') {
         
           steps {
              
                sh 'docker build -t javawebapp:latest .' 
                sh 'docker tag javawebapp bhushanshete/javawebapp:latest'     
          }
        }
     
   stage('Login to DockerHub') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
	
    stage('Push Image to dockerHUb') {
      steps {
        sh 'docker push bhushanshete/javawebapp:latest'
      }
	  post {
    always {
      sh 'docker logout'
    }
  }
    
	}
	
	
  }
  
       
   
      
 }

pipeline{
  agent  any
   environment {
        DOCKER_IMAGE_NAME = "my-image:${env.BUILD_NUMBER}"
    }
  stages{
    stage('Clone Repo') {
      steps{
      git 'https://github.com/malekalghraba/Jenkins-Test.git'
        }}
 
    stage('Build Project') {
      steps{
        script{
      sh "mvn clean"
      sh "mvn package"
      sh "mvn install"
    }
    }
    }
    
    
    stage('Build Docker Image') {
      steps{
        script {
      sh "docker  build -t DOCKER_IMAGE_NAME  ."
    }
      }}
    stage('Deploy Docker Image'){
      steps{
        script {
	   sh "docker run --name DOCKER_IMAGE_NAME -d -p 2222:2222 DOCKER_IMAGE_NAME}"
               }
            }
                                }
 }
}

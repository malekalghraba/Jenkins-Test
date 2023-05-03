pipeline{
  agent  any
   environment {
   
    dockerImage
    dockerImageTag = "devopsexample${env.BUILD_NUMBER}"
    
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
        sh "docker  build -t devopsexample:${env.BUILD_NUMBER} ."
    }
      }}
    stage('Deploy Docker Image'){
      steps{
        script {
	  sh "docker run --name devopsexample -d -p 2222:2222 devopsexample:${env.BUILD_NUMBER}"
               }
            }
                                }
 }
}

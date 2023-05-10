pipeline{
  agent  any
   environment {
  
    dockerImageTag = "devopsexample${env.BUILD_NUMBER}"
    
    }
  stages{
    stage('Clone Repo') {
      steps{
      git 'https://github.com/malekalghraba/Jenkins-Test.git'
        }}

       stage('Run SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn clean install sonar:sonar'
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

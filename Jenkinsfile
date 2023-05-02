pipeline{
  agent  any
  stages{
    stage('Clone Repo') {
      steps{
      git 'https://github.com/malekalghraba/Jenkins-Test.git'
        }}
 stage('SonarQube analysis') {
   steps{
        script{
    withSonarQubeEnv(credentialsId: 'f225455e-ea59-40fa-8af7-08176e86507a', installationName: 'My SonarQube Server') { // You can override the credential to be used
      sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
    }}}
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
      sh "docker  build -t devopsexample:${env.BUILD_NUMBER}  ."
    }
      }}
    stage('Deploy Docker Image'){
      steps{
        script {
	      echo "Docker Image Tag Name: ${dockerImageTag}"
	      sh "docker run --name devopsexample -d -p 2222:2222 devopsexample:1.0"
               }
            }
                                }
 }
}
}
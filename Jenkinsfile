pipeline{

  agent any

  stages{
    stage('git checkout'){
      steps{
      }
    }
  }
  stage ('unit testing') {
    
    steps {
      sh 'mvn test'
    }
  }
  stage ('Intergration testing') {
    steps {
      sh 'mvn verify - oski unit test'
    }
  }
  stage ('maven build') {
    steps {
      sh 'mvn clean install'
    }
  }
  stage ('static code analysis') {
    steps {
      scripts {
        withSonarQubeEnv(credentialsId: 'sonar-token') {
         sh 'mvn clean package sonar:sonar'
}
      }
    }
  }
  stage ('qulity gate status') {
    steps{
      scripts{
        waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
      }
    }
  }
} 
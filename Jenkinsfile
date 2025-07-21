

pipeline{
  agent any
  tools {
    maven 'maven3.9'
  }
  stages {
    stage('Git Clone'){
      steps{
        git branch: 'main', url: 'https://github.com/ifediniru/docker_local.git'
      }
    }
    // stage('Build containers'){
    //   steps{
    //     sh 'docker-compose up -d'
    //   }
    // }
    // stage('Initializing container'){
    //   steps{
    //     sh 'echo waiting for all container services to be up'
    //     sh 'sleep 60'
    //   }
    // }
    stage('Execute maven package'){
      steps{
        echo 'package artifact'
        sh 'mvn clean package'
      }
    }
    stage('Test artifact with sonar'){
      steps{
        sh 'echo mvn sonar:sonar'
      }
    }
    stage('Deploy to nexus'){
      steps{
        sh 'mvn deploy -s ./settings.xml'
      }
    }
   stage('Tomcat'){
     steps {
      echo 'Pushing to Tomcat'
        deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://172.31.36.205:8080/')], contextPath: null, war: 'target/*war'
         echo 'Done'
     }
    }
  }
}
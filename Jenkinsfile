pipeline {
  agent any
  
  triggers {
    pollSCM('* * * * *')
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main',
        url: 'https://github.com/gskohot72/source-maven-java-spring-hello-webapp.git'
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean package -DskipTests=true'
      }
    }
    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }
    stage('Deploy') {
      steps {
        deploy adapters: [tomcat9(credentialsId: 'tomcat-manager', url: 'http://ec2-3-35-157-202.ap-northeast-2.compute.amazonaws.com:8080/')], contextPath: null, war: 'target/hello-world.war'
      }
    }
  
  }

}

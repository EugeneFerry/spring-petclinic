pipeline {
  agent {
    node {
      label 'whatever'
    }
    
  }
  stages {
    stage('Build') {
      agent {
        docker {
          reuseNode true
          image 'maven:3.5.0-jdk-8'
          args '-v /root/.m2:/root/.m2'
        }
        
      }
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('Build and Publish Image') {
      steps {
        sh '''
          docker build -t eugeneferry/spring-petclinic:latest .
        '''
      }
    }
  }
}
pipeline {
  agent none
  stages {
    stage('Build') {
      agent {
        docker {
          image 'maven:3-alpine'
          args 'args \'-v /root/.m2:/root/.m2\''
        }
        
      }
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('Docker Build') {
      agent {
        docker {
          image 'Docker'
        }
        
      }
      steps {
        sh 'docker build -t eugeneferry/spring-petclinic:latest .'
      }
    }
  }
}
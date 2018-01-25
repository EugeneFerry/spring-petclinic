pipeline {
  agent none
  stages {
    stage('Build') {
      agent {
        docker {
          image 'maven:3-alpine'
        }
        
      }
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('Docker Build') {
      agent any
      steps {
        sh 'docker build -t eugeneferry/spring-petclinic:latest .'
      }
    }
  }
}
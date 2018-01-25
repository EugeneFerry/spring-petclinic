pipeline {
  agent {
    docker {
      image 'docker'
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
    stage('Docker Build') {
      steps {
        sh 'docker build -t eugeneferry/spring-petclinic:latest .'
      }
    }
    stage('Docker Push') {
      steps {
        withCredentials(bindings: [usernamePassword(credentialsId: 'credentials-id', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push shanem/spring-petclinic:latest'
        }
        
      }
    }
  }
}
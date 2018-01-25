pipeline {
  agent {
    docker {
      image 'maven:3-alpine'
      args '-v /root/.m2:/root/.m2'
    }
    
  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('Docker Build') {
	  steps {
		 script {
			docker.withTool('docker') {
					def app = docker.build("eugenef/spring-petclinic:latest")
					echo "Push to Docker repository ..."
			}
         }
	  }
    }
  }
}
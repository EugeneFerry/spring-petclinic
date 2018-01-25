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
	stage('Test') {
	  agent {
        docker {
          reuseNode true
          image 'maven:3.5.0-jdk-8'
          args '-v /root/.m2:/root/.m2'
        }
      }
	  steps {
	 	sh 'mvn test'
	  }
	  post {
		always {
			junit 'target/surefire-reports/*.xml'
	    }
	  }
    }
    stage('Docker Build') {
      steps {
        sh 'docker build -t eugeneferry/spring-petclinic:1.0.0 .'
      }
    }
	stage('Docker Push') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'credentials-id', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push eugeneferry/spring-petclinic:1.0.0'
		}
      }
    }
  }
}
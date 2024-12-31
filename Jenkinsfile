pipeline {
  agent any

	tools {
     maven 'Maven 3.9.9'
	}
	
  stages {
    stage("one") {
      steps {
        echo 'compiling'
	      sh 'mvn compile'
      }
    }
    stage("running unit tests") {
      steps {
        sh 'mvn clean test'
      }
    }
    stage("packaging the app") {
      steps {
        sh 'mvn package -DskipTests'
      }
    }
  }

  post {
    always {
      echo 'This pipeline is completed...'
    }
  }
}

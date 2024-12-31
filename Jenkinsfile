pipeline {
  agent any
  stages {
    stage('one') {
      steps {
        echo 'compiling'
        sh 'mvn compile'
      }
    }

    stage('running unit tests') {
      steps {
        sh 'mvn clean test'
      }
    }

    stage('packaging the app') {
      steps {
        sh '''# Truncate the GIT_COMMIT to the first 7 characters
GIT_SHORT_COMMIT=$(echo $GIT_COMMIT | cut -c 1-7)

# Set the version using Maven
mvn versions:set -DnewVersion="$GIT_SHORT_COMMIT"
mvn versions:commit
'''
        sh 'mvn package -DskipTests'
        archiveArtifacts '**/targets/*.jar'
      }
    }

  }
  tools {
    maven 'Maven 3.9.9'
  }
  post {
    always {
      echo 'This pipeline is completed...'
    }

  }
}
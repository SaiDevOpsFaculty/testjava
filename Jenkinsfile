pipeline {
  agent any
  stages {
    stage('compile') {
      steps {
        git 'https://github.com/Debasish96/time-tracker.git'
        sh '/opt/maven/apache-maven-3.6.3/bin/mvn compile'
      }
    }
	stage('test') {
      steps {
	    sh '/opt/maven/apache-maven-3.6.3/bin/mvn test'
	  }
	  post {
        always {
          archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
          junit 'build/reports/**/*.xml'
        }
      }
	}
	stage('package') {
	  steps {
	    sh '/opt/maven/apache-maven-3.6.3/bin/mvn clean package'
	  }
	}
  }
}

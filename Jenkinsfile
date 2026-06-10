pipeline {
	agent any

	triggers {
		githubPush()
		}

	tools {
		maven 'maven.3.9.16'
		}		

	stages {

	stage('Clone Git') {
		steps {
 			echo 'Cloning source code from Git'

 			git branch: 'main' , url: 'https://github.com/praveensipala/Devops.git'
	 	}
 	}

	stage('Build with Maven'){
		steps {
			echo 'Building with Maven'

			sh 'mvn clean package'
			}
		}
	
	stage('SonarQube Analysis'){
		steps {
			echo 'Analyzing with SonarQube'

			sh 'mvn sonar:sonar'
			}
		}

	stage('Deploy to Nexus'){
		steps {
			echo 'Deploying to Nexus'

			sh 'mvn deploy'
			}
		}

	stage('Deploy to Tomcat'){
		steps {
			echo 'Deploying to Tomcat'

			deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat', path: '', url: 'http://54.224.107.225:8080/')], contextPath: 'love-test', war: '**/*.war'
			}
		}

	}

post{
	always {
		echo 'pipeline completed'
		}
	
	success {
		echo ' Build ${BUILD_NUMBER} OF THE JOB ${JOB_NAME} COMPLETED SUCCESSFULLY '
		}

	failure {
		echo ' Build ${BUILD_NUMBER} OF THE JOB ${JOB_NAME} FAILED CHECK CONSOLE LOGS IN ${BUILD_URL} '
		}
	}
}
		


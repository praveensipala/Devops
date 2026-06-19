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

			deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat', path: '', url: 'http://100.56.231.117:8080/')], contextPath: 'my_love_app', war: '**/*.war'
			}
		}

	}

	post {

		always {
			echo "========================================="
			echo "Pipeline execution completed."
			echo "Job Name      : ${env.JOB_NAME}"
			echo "Build Number  : ${env.BUILD_NUMBER}"
			echo "Build Result  : ${currentBuild.currentResult}"
			echo "Build URL     : ${env.BUILD_URL}"
			echo "========================================="
		}

		success {
			echo "SUCCESS: Build #${env.BUILD_NUMBER} of '${env.JOB_NAME}' completed successfully."
		}

		failure {
			echo "FAILURE: Build #${env.BUILD_NUMBER} of '${env.JOB_NAME}' failed."
			echo "Console Log: ${env.BUILD_URL}console"
		}

		unstable {
			echo "UNSTABLE: Build #${env.BUILD_NUMBER} is unstable."
		}

		aborted {
			echo "ABORTED: Build #${env.BUILD_NUMBER} was aborted."
		}

		cleanup {
			cleanWs()
		}
	}
}
		


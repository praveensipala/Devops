pipeline {
    agent any
    stages {
        stage ('clone SCM'){
        steps {
            echo 'this stage is clone SC from Git-Hub'
            git branch: 'main', url: 'https://github.com/praveensipala/Devops.git'
            
            }
        }
        stage ('Build Artifact') {
            steps {
                echo 'This stage is builds the code using Maven'
                sh 'mvn clean install'
            }
        }
        
        stage ('Deploy in Tomcat') {
            steps {
                echo 'This stage is deploy .war file in Tomcat'
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat', path: '', url: 'http://3.87.115.254:8080/')], contextPath: 'first-pipeline', war: '**/*.war'
            }
        }
        
    }
}


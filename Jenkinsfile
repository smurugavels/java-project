pipeline {
    agent any
	stages {
		stage('Test') {
			steps {
						git 'https://github.com/rclc/java-project.git'
		sh 'ant -buildfile test.xml'   

			}
	}   
	stage('Build') {    
		steps {sh 'ant'}   
	}   
	stage('Results') {
		steps {
			junit 'reports/*.xml'
		}
	}
	}
}

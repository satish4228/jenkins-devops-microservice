
//Scipted Syntax
// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage('Integration Test') {
// 		echo "Integration Test"
// 	}
// }

//Declarative Syntax
pipeline {
	//agent any
	agent { docker { image 'maven:3.6.3'}
	stages {
		stage('Build') {
			steps {
				sh 'mvn --version'
				echo "Build"
			}
		}

		stage('Test') {
			steps {
				echo "Test"
			}
		}
	} 

	post {
		always {
			echo "Always I will run"
		}
		success {
			echo "When Success"
		}
		failure {
			echo "When failure"
		}
	}	
}
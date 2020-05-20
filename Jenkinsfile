
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
	agent any
	environment {

		// We want to take Home Path for boot the tools
		// Add to Our Environment path
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		// This will add both maven and docker bin folder path to the our env path
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"  
	}
	//agent { docker { image 'maven:3.6.3'} }
	stages {
		stage('Build') {
			steps {
				sh 'mvn --version'
				sh 'docker version'
				echo "$PATH"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
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
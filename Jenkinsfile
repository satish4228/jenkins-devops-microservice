
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
		stage('CheckOut') {
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

		stage('Compile') {
			steps {
				sh 'mvn clean install'
			}
		}

		stage('Test') {
			steps {
				sh 'mvn test'
			}
		}
		stage('Integration test') {
			steps {
				sh 'mvn failsafe:integration-test failsafe:verify'
			}
		}
		stage('Build Docker Image') {
			steps {
				// This is the Declarative way of calling
				// sh 'docker build -t satish4228/currency-exchange-service-from-jenkins:$env.BUILD_TAG'

				//The above can be achived by using the function aswell.
				script{
					dockerImage = docker.build("satish4228/currency-exchange-service-from-jenkins:${env.BUILD_TAG}")
				}
			}
		}

		//But Jenkins want to connect your docker hub
		stage ('package') {
			steps{
				script{
					sh 'mvn package -DskipTests'
				}
			}
		}


		stage('Push Docker Image'){
			steps {
				script{

					docker.withRegistry ('', 'dockerhub') {

					
					dockerImage.push();
					//For a latesh push use 
					dockerImage.push('latest')
					}
				}
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
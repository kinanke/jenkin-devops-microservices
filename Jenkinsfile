//Declarative
pipeline {
	agent any
	// agent {docker { image 'python:alpine3.10'} }
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage ('Checkout') {
			steps {
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo " BUILD_NUMBER - $env.BUILD_NUMBER"
				echo " BUILD_ID- $env.BUILD_ID"
			}
		}
		stage ('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage ('Test') {
			steps {
				sh "mvn test"
			}
		}
		stage ('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage ('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage ('Docker Build') {
			steps {
				//sh "docker build -t kinanke/currancy-exchange-devops:$env.BUILD_TAG ."
				script {
					dockerImage = docker.build("kinanke/currancy-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage ('Docker Push') {
			steps {
				script{
					docker.withRegistry('','dockerhub'){
						dockerImage.push();
						dockerImage.push('latest');	
					}

				}
			}
		}	
	}
}

// //Scripted
// node {
// 	echo "Build"
// 	echo "Test"
// 	echo "Integration Test"
// }

//Normal
// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage('Integration Test') {
// 		echo "Test"
// 	}
// }

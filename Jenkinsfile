//Declarative
pipeline {
	// agent any
	agent {docker { image 'python:alpine3.10'} }
	stages {
		stage ('Build') {
			steps {
				sh 'python3 --version'
				echo "Build"
			}
		}
		stage ('Test') {
			steps {
				echo "Test"
			}
		}
		stage ('Integration Test') {
			steps {
				echo "Integration Test"
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

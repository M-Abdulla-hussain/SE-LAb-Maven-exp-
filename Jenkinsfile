pipeline {
	agent any

	tools {
		jdk 'JAVA_HOME'
		maven 'MAVEN_HOME'
	}

	options {
		timestamps()
		ansiColor('xterm')
	}

	stages {
		stage('Checkout') {
			steps {
				echo 'Cloning repository'
				deleteDir()
				git branch: 'main', url: 'https://github.com/M-Abdulla-hussain/SE-LAb-Maven-exp-.git'
			}
		}
		stage('Clean') {
			steps {
				echo 'Cleaning project'
				bat 'mvn -B clean'
			}
		}
		stage('Compile') {
			steps {
				echo 'Compiling sources'
				bat 'mvn -B compile'
			}
		}
		stage('Unit Tests') {
			steps {
				echo 'Running unit tests'
				bat 'mvn -B test'
			}
		}
		stage('Package') {
			steps {
				echo 'Packaging application'
				bat 'mvn -B package'
				archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
			}
		}
		stage('Run App') {
			steps {
				echo 'Executing application main class'
				bat 'java -cp target/hghg-0.0.1-SNAPSHOT.jar success.hghg.App'
			}
		}
		stage('Final') {
			steps {
				echo 'Pipeline completed successfully.'
			}
		}
	}

	post {
		success {
			echo 'SUCCESS: Build and run completed.'
		}
		failure {
			echo 'FAILURE: Check logs.'
		}
		always {
			junit 'target/surefire-reports/*.xml'
		}
	}
}

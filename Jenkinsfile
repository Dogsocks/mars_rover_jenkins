pipeline {
    agent any
	
	environment {
		registry = "dogsocks/mars_rover"
        	registryCredential = 'dockerhub'
        	dockerImage = ''
	}	
	
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Project Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/master']],
                    userRemoteConfigs: [[url: 'https://github.com/Dogsocks/Mars-Rovers-Site.git']]
                ])
            }
        }
		
        stage('Unit Test'){
            steps {
                echo 'Unit tests starting'
                sh 'ls'
                sh 'cd mars_rover; python3 -m unittest unit_tests.test_rovers'
            }
        }
		
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":latest" 
                }
            }
        }
		
        stage('Mail to Dockerhub') {
            steps {
		    echo 'Dockerhub push starting'
                script {
                    docker.withRegistry( '', registryCredential ){
                        dockerImage.push()
                    }
                }

            }
        }
    }
	post {
		always {
			sh 'docker logout'
		}
	}
}

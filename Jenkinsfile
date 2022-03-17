pipeline {
    agent any
	
	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
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
                sh 'cd mars_rover; python -m unittest unit_tests.test_rovers'
            }
        }
		
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t dogsocks/mars_rover:latest .'
            }
        }
		
        stage('Mail to Dockerhub') {
            steps {
				sh 'docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin | docker push docker pull dogsocks/mars_rover:latest'

            }
        }
    }
	post {
		always {
			sh 'docker logout'
		}
	}
}

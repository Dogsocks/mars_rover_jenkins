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
                sh 'cd mars_rover; python3 -m unittest unit_tests.test_rovers'
            }
        }
		
        stage('Build Docker Image') {
            steps {
                sh 'docker buildx build -t dogsocks/mars_rover:latest . --platform linux/amd64'
            }
        }
		
        stage('Mail to Dockerhub') {
            steps {
				sh 'docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin | docker push dogsocks/mars_rover:latest'

            }
        }
    }
	post {
		always {
			sh 'docker logout'
		}
	}
}

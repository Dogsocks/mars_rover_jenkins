pipeline {
    agent any
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
                echo 'Hello World'
                sh 'make check || true'
                junit '**/target/*.xml'
            }
        }
        stage('Regression Test'){
            steps {
                echo 'Hello World'
            }
        }
        stage('Deploy') {
            steps {
                echo 'make publish'
            }
        }
    }
}

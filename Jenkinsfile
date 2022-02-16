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
                echo 'Unit tests starting'
                sh 'ls'
                sh 'cd mars_rover; python -m unittest unit_tests.test_rovers'
            }
        }
        stage('Regression Test'){
            steps {
                sh script: '''
                cd Regression_testing/features; python behave mars_rover_regression.feature
                '''

            }
        }
        stage('Deploy') {
            steps {
                echo 'make publish'
            }
        }
    }
}

pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Code Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/master']], 
                    userRemoteConfigs: [[url: 'https://github.com/Dogsocks/Mars-Rovers-Site.git']]
                ])
            }
        }
            }
        stage('Unit Test'){
            steps {
                echo 'Hello World'
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

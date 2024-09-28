//SCRIPTED

//DECLARATIVE
pipeline {
    //agent any
    agent {
        /* docker {
            image 'maven:3.9.9'
            args '-v /root/.m2:/root/.m2'
        } */
        docker { image 'node:14' }
    }
    stages {
        stage('Build') {
            steps {
                //sh 'mvn --version'
                sh 'node --version'
                echo "Build"
            }
        }
        stage('Test') {
            steps {
                echo "Test"
            }
        }
        stage('Integration Test') {
            steps {
                echo "Integration Test"
            }
        }
    }
    post {
        always {
            echo 'Im awesome. I run always'
        }
        success {
            echo 'I run when you are successful'
        }
        failure {
            echo 'I run when you are failed'
       }
    }
}

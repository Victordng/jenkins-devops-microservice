//SCRIPTED

//DECLARATIVE
pipeline {
    agent any
//     agent {
        /* docker {
            image 'maven:3.9.9'
            args '-v /root/.m2:/root/.m2'
        } */
//         docker { image 'node:14' }
//     }
    environment {
        dockerHome = tool 'myDocker'
        mavenHome = tool 'myMaven'
        PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
    }
    stages {
        stage('Checkout') {
            steps {
                sh 'mvn --version'
                sh 'docker version'
                echo "Build"
                echo "PATH - $PATH"
                echo "BUILD_NUMBER - $env.BUILD_NUMBER"
                echo "BUILD_ID - $env.BUILD_ID"
                echo "JOB_NAME - $env.JOB_NAME"
                echo "BUILD_TAG - $env.BUILD_TAG"
                echo "BUILD_URL - $env.BUILD_URL"
            }
        }
//         stage('Compile') {
//             steps {
//                 sh "mvn clean compile"
//             }
//         }
//         stage('Test') {
//             steps {
//                 sh "mvn test"
//             }
//         }
//         stage('Integration Test') {
//             steps {
//                 sh "mvn failsafe:integration-test failsafe:verify"
//             }
//         }
        stage('Package') {
            steps {
                sh "mvn package -DskipTests"
            }
        }
        stage('Build Docker Image') {
            steps {
                //docker build -t vdongmo/currency-exchange-devops:${env.BUILD_TAG} .
                script {
                    dockerImage = docker.build("vdongmo/currency-exchange-devops:${env.BUILD_TAG}")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                //docker push vdongmo/currency-exchange-devops:${env.BUILD_TAG}
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerImage.push();
                        dockerImage.push('latest');
                    }
                }
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

pipeline {
    agent any

    tools {
        jdk 'jdk-11'         // Ensure JDK version
        maven 'maven-3.8.8'  // Ensure Maven version
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/tanmaygupta7781/MvnApp.git', branch: 'master'
            }
        }

        stage('Environment Check') {
            steps {
                sh 'echo $PATH'
                sh 'java -version'
                sh 'mvn -version'
            }
        }

        stage('Build') {
            steps {
                script {
                    try {
                        sh 'mvn clean package -X'  // Debugging build command
                    } catch (Exception e) {
                        echo "Build failed: ${e.getMessage()}"
                        currentBuild.result = 'FAILURE'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Run Application') {
            steps {
                sh 'java -jar target/*.jar'
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}

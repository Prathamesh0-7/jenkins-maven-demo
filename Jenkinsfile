pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Compile') {
            steps {
                bat 'if not exist build mkdir build'
                bat 'javac -d build src\\main\\java\\com\\example\\App.java'
            }
        }

        stage('Test Application') {
            steps {
                bat 'java -cp build com.example.App'
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                    if not exist deployed mkdir deployed
                    copy /Y build\\com\\example\\App.class deployed\\App.class
                '''
                echo 'Application deployed successfully!'
            }
        }
    }

    post {
        success {
            echo 'EXPERIMENT 8: SUCCESS'
        }
        failure {
            echo 'Build or deployment failed. Check Console Output.'
        }
    }
}

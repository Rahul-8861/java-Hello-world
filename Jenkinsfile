pipeline {
    agent any

    environment {
        // Define environment variables here if needed
        MY_ENV = "value"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/siddarth9899/CS9899'
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                // Add your build commands here
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Add your test commands here
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Add your deploy steps here
            }
        }
    }
}

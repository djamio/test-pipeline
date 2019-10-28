pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('npm install') {
            steps {
                sh 'npm install'
                echo 'npm install..'
            }
        }

        stage('Test') {
            steps {
                sh 'ng test'
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
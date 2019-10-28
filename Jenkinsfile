pipeline {
    agent any

    stages {

        stage ('checkout'){
            steps{
            checkout scm
            }
        }   

        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        
        stage ('code quality'){
      steps{
                sh 'npm run ng lint'
      }
    }
    

        stage('Test') {
            steps {
                sh 'npm run ng build
'
                echo 'Testing..'
            }
        }

        stage('npm install') {
            steps {
                sh '''
                    npm install --verbose -d 
                    npm install --save classlist.js
                '''
                echo 'npm install ..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
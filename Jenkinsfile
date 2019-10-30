pipeline {
    agent any

    parameters {
        string(defaultValue: "TEST", description: 'What environment?', name: 'userFlag')
        choice(choices: ['US-EAST-1', 'US-WEST-2'], description: 'What AWS region?', name: 'region')
    }

    stages {

        stage ('checkout'){
            steps{
            checkout scm
            }
        }   

     
    
    //  stage('npm install') {
    //         steps {
    //             sh '''
    //                 npm install --verbose -d 
    //                 npm install --save classlist.js
    //             '''
    //             echo 'npm install ..'
    //         }
    //     }

    //     stage('build') {
    //         steps {
    //             sh 'npm run ng -- build'
    //             echo 'building..'
    //         }
    //     }


        stage('Test') {
            steps {
                sh ''' 

                export CHROME_BIN=/usr/bin/chromium-browser
                npm run ng -- test --code-coverage --browsers ChromeHeadless
                '''
                echo 'Testing..'
            }
        }

            
        stage ('code quality'){
      steps{
                sh 'npm run ng -- lint'
      }
    }

       
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
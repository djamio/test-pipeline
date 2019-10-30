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

     
    
     stage('npm install') {
            steps {
                sh '''
                    npm install --verbose -d 
                    npm install --save classlist.js
                '''
                echo 'npm install ..'
            }
        }

    //     stage('build') {
    //         steps {
    //             sh 'npm run ng -- build'
    //             echo 'building..'
    //         }
    //     }


        stage('Test') {
            steps {
                echo 'Testing..'
                sh ''' 
                export CHROME_BIN=/usr/bin/chromium-browser
                npm run ng -- test --code-coverage --browsers ChromeHeadless
                '''
            }
            post {
                always {
                    junit 'reports/karma/HeadlessChrome_77.0.3865_(Ubuntu_0.0.0)/report.xml'
                }
            }
            post {
                always {
                    publishHTML target: [
                        allowMissing         : false,
                        alwaysLinkToLastBuild: false,
                        keepAll             : true,
                        reportDir            : 'coverage/test-pipeline',
                        reportFiles          : 'index.html',
                        reportName           : 'Test Report'
                    ]
                }
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
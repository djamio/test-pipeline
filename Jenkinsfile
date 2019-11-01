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

     stage('build docker') {
            steps {
                sh '''
                    docker build .
                '''
                echo 'docker build ..'
            }
        }


stage('Build Docker Image'){
                steps {

    sh 'docker build -t djamio/test-docker:0.0.1 .'
  }
  }

//   stage('Upload Image to DockerHub'){
//     withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerHubPwd')]) {
//       sh "docker login -u djamio -p ${password}"
//     }
//     sh 'docker push djamio/test-docker:0.0.1'
//   }
  stage('Remove Old Containers'){
                  steps {

    sshagent(['test-docker-dev']) {
      try{
        def sshCmd = 'ssh -o StrictHostKeyChecking=no ec2-user@172.31.18.198'
        def dockerRM = 'docker rm -f test-docker'
        sh "${sshCmd} ${dockerRM}"
      }catch(error){

      }
    }
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
                echo 'Testing..'
                sh ''' 
                export CHROME_BIN=/usr/bin/chromium-browser
                npm run ng -- test --code-coverage --browsers ChromeHeadless
                '''
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
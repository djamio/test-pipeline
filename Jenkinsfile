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



// stage('Stop running image') {

//             steps {
//                 def ret

//                 sh '''
//                     docker stop $(docker ps -a -q)
//                     docker rm $(docker ps -a -q)
//                 '''
//                 echo 'stop image ..'
//             }
//         }



stage('build docker') {
            steps {
                sh '''
                    docker build -t djamio/docker-test:1.0 .
                '''
                echo 'docker build install ..'
            }
        }


stage('run docker image') {
            steps {
                sh '''
                    docker run  -d -p 80:80 djamio/docker-test:1.0
                '''
                echo 'run docker image ..'
            }
        } 
        

stage('push docker image to dockerhub') {
            steps {
                // sh '''
        

withCredentials([[
    $class: 'UsernamePasswordMultiBinding',
                   credentialsId : 'dockerhub',                                                 
                   secretKeyVariable: 'KEY_1'
                                     ]]) { 
                                         
                        sh '''
                            docker login -u djamio/docker-test -p ${KEY_1}
                        '''
                                      }
                                      sh '''
            docker push djamio/docker-test:2.0.0
                                      '''

                // '''
                echo 'run docker image ..'
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
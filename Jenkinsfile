   node {
    def nodeHome = tool name: 'node-11.0.0', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
    env.PATH = "${nodeHome}/bin:${env.PATH}"


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

        stage('build') {
            steps {
                sh 'npm run ng -- build'
                echo 'building..'
            }
        }


        stage('Test') {
            steps {
                sh 'npm run ng -- test'
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
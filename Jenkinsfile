pipeline {
    agent {
        label 'AGENT-1'
    } 
    options{
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()

    }

    environment{
        DEBUG='true'
        appVersion='' // this is global varibale you can use this across pipeline.
    }

    stages {
        stage("Read the version"){
            steps{
                script{
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo "App Version: ${appVersion}"
                }
                
            }
        }

        stage("Install Dependencies"){
            steps{
                sh 'npm install'

            }
        }

        stage("Build Images")
        {
            steps{
                
                sh """
                docker build -t manohar1481/backend:${appVersion} .
                docker images
                """

            }
        }
    }
    post{
        always{
            echo "This section runs Always"
            deleteDir()
        }
        success{
            echo "This section runs when job got success"
        }
        failure{
            echo "This section runs when job got failure"
        }
    }

}
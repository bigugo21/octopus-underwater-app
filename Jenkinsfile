pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
         stage('https://github.com/bigugo21/octopus-underwater-app') { 
            steps { 
                script{
                checkout scm
                }
            }
        }

        stage('Build') { 
            steps { 
                script{
                 app = docker.build("underwater")
                }
            }
        }
        stage('Test'){
            steps {
                 echo 'Empty'
            }
        }
        stage('Deploy') {
            steps {
                script{
                        docker.withRegistry('https://535407588590.dkr.ecr.us-west-2.amazonaws.com/ugocothrepo', 'ecr:us-west-2:aws-credentials') {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                    }
                }
            }
        }
    }
}

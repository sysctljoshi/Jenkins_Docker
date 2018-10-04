#!/usr/bin/env groovy
pipeline {
    agent any
    
    stages{
        stage('Build'){
         steps{
             sh "/usr/local/apache-maven-3.0.5/bin/mvn clean package"
         }
         post {
             success {
                 echo 'now Archiving'
                 archiveArtifacts artifacts: '**/target/*.war'
             }
         }

        }
        stage ('Deploy to Staging'){
            steps {
                build job: 'Deploy-to-staging'
            }
     
        }

        stage ('Deploy to Production'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }

                build job: 'deploy-to-Prod'
            }
            post {
                success {
                    echo 'Code deployed to Production.'
                }

                failure {
                    echo ' Deployment failed.'
                }
            }
}


    }
}
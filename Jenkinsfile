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
        
    }
}
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '3')), pipelineTriggers([cron('* * * * *')])])
pipeline{
    agent any
    tools{
        maven "maven"
    }//tools closing
    properties([parameters([choice(choices: ['main ', 'stg', 'prod'], name: 'branches')])])
    stages{
        stage("Getting code from git"){
            steps{
                git branch: "${branches}", url: 'https://github.com/penmetsa123/vprofile-project.git'
            }
        }
        stage("packaging the code"){
            steps{
                sh "mvn clean package"
            }
        }

    }//stages closing
}//Closing pipeline



pipeline{
    agent any
    tools{
        maven "maven"
    }//tools closing
    stages{
        stage("Getting code from git"){
            steps{
                git branch: "main", url: 'https://github.com/penmetsa123/vprofile-project.git'
            }
        }
        stage("packaging the code"){
            steps{
                sh "mvn clean package"
            }
        }

    }//stages closing
}//Closing pipeline



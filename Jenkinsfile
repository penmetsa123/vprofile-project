pipeline {
    agent any

    tools {
        maven 'maven'  // Ensure Maven is correctly configured in Jenkins
    }

    stages {
        stage('Get the Git Code') {
            steps {
                git branch: 'main', url: 'https://github.com/penmetsa123/vprofile-project.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Quality Test') {
            steps {
                sh 'mvn sonar:sonar'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sshagent(['tomcat']) {
                    sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@13.203.208.170:/opt/tomcat/webapps/'
                }
            }
        }
    }
}



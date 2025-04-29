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
         stage('build') {
            steps {
               sh 'mvn package'
            }
         stage('Quality test') {
            steps {
               sh 'mvn sonar:sonar'
            }
        }
    }
}
}

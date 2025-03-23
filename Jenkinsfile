pipeline {
    agent Node1
    tools {
        maven 'MAVEN'  // Ensure Maven is correctly configured in Jenkins
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
        }
    }
}

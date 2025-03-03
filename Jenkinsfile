pipeline {
    agent any
    tools {
        maven 'MAVEN'  // Ensure Maven is correctly configured in Jenkins
    }
    stages {
        stage('Get the Git Code') {
            steps {
                git branch: 'main', url: 'https://github.com/penmetsa123/vprofile-project.git'
            }
        }
    }
}

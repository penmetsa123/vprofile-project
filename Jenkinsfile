pipeline {
    agent any

    tools {
        maven 'MAVEN'  // This assumes that Maven is configured in Jenkins as 'MAVEN'
    }

    stages {
        stage('Get Code') {
            steps {
                // Get the code from the GitHub repository and branch 'vp-rem'
                git branch: 'vp-rem', url: 'https://github.com/devopshydclub/vprofile-project.git'
            }
        }

        stage('Package the Code') {
            steps {
                // Run the Maven build to package the code
                sh "${tool 'MAVEN'}/bin/mvn clean package"
            }
        }
         stage('Deploy to Tomcat') {
            steps {
                script {
                    // Deploy WAR file to Tomcat using SCP or another method
                    sh """
                    scp target/vprofile-v2.war ubuntu@172.31.13.158:/opt/tomcat/webapps
                    """
                }
            }
        }
    }
}

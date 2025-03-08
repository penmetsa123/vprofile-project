pipeline {
    agent any

    environment {
        TOMCAT_HOST = '172.31.13.158'               // IP address of the Tomcat server
        TOMCAT_USER = 'ubuntu'                      // The user on the remote server
        TOMCAT_WEBAPPS_DIR = '/opt/tomcat/webapps'  // The directory where WAR files go
        WAR_FILE = 'target/vprofile-v2.war'         // Path to the WAR file
    }

    tools {
        maven 'MAVEN'  // Maven tool configured in Jenkins
    }

    stages {
        stage('Get Code') {
            steps {
                git branch: 'vp-rem', url: 'https://github.com/devopshydclub/vprofile-project.git'
            }
        }

        stage('Package the Code') {
            steps {
                sh "${tool 'MAVEN'}/bin/mvn clean package"
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    // Using the sshagent to inject the SSH private key stored in Jenkins credentials
                    sshagent(['my-ssh-key']) {  // Replace 'my-ssh-key' with the actual credentials ID
                        // SCP the WAR file to the Tomcat server
                        sh """
                        scp ${WAR_FILE} ${TOMCAT_USER}@${TOMCAT_HOST}:${TOMCAT_WEBAPPS_DIR}
                        """
                    }
                }
            }
        }

        stage('Restart Tomcat') {
            steps {
                script {
                    // Restart Tomcat after deploying the WAR file
                    sshagent(['c48d6548-095c-42d2-a6e2-05b31f4ae898']) {  // Replace 'my-ssh-key' with the actual credentials ID
                        sh """
                        ssh ${TOMCAT_USER}@${TOMCAT_HOST} 'sudo systemctl restart tomcat'
                        """
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment was successful!'
        }
        failure {
            echo 'Deployment failed. Check the logs for errors.'
        }
    }
}



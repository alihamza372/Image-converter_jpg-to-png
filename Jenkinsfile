pipeline {
    agent any
    triggers {
        pollSCM('*/5 * * * *')
    }
    environment {
        TOMCAT_WEBAPPS_DIR = '/home/ali/Desktop/tomcat/webapps/Image-converter_jpg-to-png'
    }
    stages {
        stage('Fetch Code') {
            steps {
                // Checkout code from GitHub
                git branch: 'master', url: 'https://github.com/alihamza372/jpg_to_png.git'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    // Display current user
                    sh 'whoami'

                    // Print environment variables
                    sh 'env'

                    // Ensure the directory exists
                    sh "sudo mkdir -p ${TOMCAT_WEBAPPS_DIR}"
                    
                    // Set ownership to Jenkins user
                    sh "sudo chmod -R 777 ${TOMCAT_WEBAPPS_DIR}"

                    // Copy files to Tomcat webapps directory
                    sh "cp -r * ${TOMCAT_WEBAPPS_DIR}/"
                }
            }
        }

        stage('Restart Tomcat') {
            steps {
                // Restart Tomcat (replace 'tomcat' with your Tomcat service name)
                sh 'sudo systemctl restart tomcat'
            }
        }
    }
}


pipeline {
    agent any
    triggers {
        pollSCM('*/5 * * * *')
    }
    environment {
        TOMCAT_WEBAPPS_DIR = '/opt/tomcat/webapps/Image-converter_jpg-to-png'
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
                    
                    // Set ownership to Jenkins user
                    //sh "chmod -R 777 ${TOMCAT_WEBAPPS_DIR}"
                    // Ensure the directory exists
                    sh "mkdir -p ${TOMCAT_WEBAPPS_DIR}"
                    // Copy files to Tomcat webapps directory
                    sh "cp -r * ${TOMCAT_WEBAPPS_DIR}/"
                }
            }
        }

        stage('Restart Tomcat') {
            steps {
                // Restart Tomcat (replace 'tomcat' with your Tomcat service name)
                sh 'systemctl start tomcat'
            }
        }
    }
}


pipeline {
    agent any
	triggers{
	pollSCM('*/5 * * * *')    
}
    stages {
        stage('Fetch Code') {
            steps {
                // Checkout code from GitHub
                git branch: 'master', url: 'https://github.com/alihamza372/jpg_to_png.git'
            }
        }
	stage('Change Directory Permissions') {
            steps {
                script {
                    // Change directory to the desired path
                    def directoryPath = '/opt/tomcat/webapps/Image-converter_jpg-to-png/'

                    // Use the 'sh' step to execute shell commands
                    // In this example, we're granting read, write, and execute permissions to all users
                    sh "chmod -R 777 ${directoryPath}"
                }
            }
        }        
        stage('Deploy to Tomcat') {
            steps {
                // Copy files to Tomcat webapps directory
                script {
                    def tomcatWebappsDir = '/opt/tomcat/webapps/Image-converter_jpg-to-png'
                    sh "rm -rf ${tomcatWebappsDir}/*"
                    sh "cp -r * ${tomcatWebappsDir}/"
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

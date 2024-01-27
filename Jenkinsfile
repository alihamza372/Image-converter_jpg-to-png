pipeline {
    agent any
	triggers{
	pollSCM('*/5 * * * *')    
    stages {
        stage('Fetch Code') {
            steps {
                // Checkout code from GitHub
                git branch: 'main', url: 'https://github.com/alihamza372/jpg_to_png.git'
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

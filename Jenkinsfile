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
        stage('Deploy to Tomcat') {
            steps {
                script {
                    def tomcatWebappsDir = '/home/ali/Desktop/tomcat/webapps/Image-converter_jpg-to-png'
			sh 'sudo chown -R jenkins:jenkins /var/tomcat/webapps/Image-converter_jpg-to-png'
			sh 'sudo chown -R jenkins:jenkins /var/tomcat/webapps'
			sh 'sudo mkdir -p /var/tomcat/webapps/Image-converter_jpg-to-png'
                    // Ensure the directory exists
                    sh "mkdir -p ${tomcatWebappsDir}"
                    
                    // Copy files to Tomcat webapps directory
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

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
            sh "sudo chown -R jenkins:jenkins ${TOMCAT_WEBAPPS_DIR}"
            sh "sudo chmod -R 755 ${TOMCAT_WEBAPPS_DIR}"
            sh "rm -rf ${TOMCAT_WEBAPPS_DIR}/*"
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


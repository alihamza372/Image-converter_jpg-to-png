pipeline {
    agent any

    stages {
        stage('Checkout from GitHub') {
            steps {
                script {
                    // GitHub repository URL
                    def gitRepoUrl = 'https://github.com/alihamza372/jpg_to_png.git'

                    // Clone the GitHub repository with the 'master' branch
                    git branch: 'master', url: gitRepoUrl
                }
            }
        }
        stage('Checking Permissions'){
        steps{
            script{
                sh 'sudo mkdir /opt/Perm'
            }
        }
        }
        stage('Display Contents') {
            steps {
                script {
                    // Display the contents of the Jenkins workspace
                    sh 'ls -la'
                }
            }
        }
    }
}

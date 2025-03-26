pipeline {
    agent any  // Use any available agent

    tools {
        maven 'Maven'  // Ensure this matches the name configured in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Hemavathipcse/MavenWebAppIntegration.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'  // Run Maven build
            }
        }

     stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint:true
            }
        }
        stage('Deploy') {
            steps {
                sh 'mvn clean package'  
                ansiblePlaybook playbook:'ansible/playbook.yml', inventory:'ansible/hosts.ini'
            }
        }

                  
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}

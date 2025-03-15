pipeline {
    agent any
    tools {
        maven 'Maven'  // Uses Jenkins-configured Maven
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/YOUR_GITHUB_USERNAME/NumberGuessGame.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                sh 'scp -i ~/Saturday.pem target/*.war ec2-user@54.227.174.111:/opt/tomcat/webapps/'
            }
        }
    }
}

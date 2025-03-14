pipeline {
    agent any
    tools {
        maven 'Maven' // Uses Jenkins-configured Maven
    }
    environment {
        SONAR_URL = 'http://your-sonarqube-server:9000' // Set your SonarQube server
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/tosinsanda/NumberGuessGame10.git'
            }
        }
        stage('Code Quality Check') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.host.url=$SONAR_URL'
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
                junit '**/target/surefire-reports/*.xml'
            }
        }
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }
        stage('Notify Team') {
            steps {
                slackSend(channel: '#devops-team', message: "Build Completed Successfully!", color: "good")
            }
        }
    }
}

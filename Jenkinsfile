pipeline {
    agent any
     
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from the GitHub repository
                git 'https://github.com/Sumukhmg/devops-oe.git'
            }
        }
        
        stage('Build') {
            steps {
                // Install dependencies and build the Node.js application
                sh 'npm install'
            }
        }
        
        stage('Test') {
            steps {
                // Run tests for your Node.js application
                sh 'npm test'
            }
        }
        
        stage('Deploy') {
            steps {
                // Build and deploy Docker container
                sh 'docker build -t my-node-microservice .'
                sh 'docker run -p 3000:3000 -d my-node-microservice'
            }
        }
    }
    
    post {
        success {
            script {
                // Send success notification to Slack
                slackSend(
                    color: '#00FF00',
                    message: "Build and deployment successful! :tada:",
                    channel: '#devops-oe-sumukh',
                    teamDomain: 'bsectionise'
                )
            }
        }
        failure {
            script {
                // Send failure notification to Slack
                slackSend(
                    color: '#FF0000',
                    message: "Build and deployment failed. :x:",
                    channel: '#your-slack-channel',
                    teamDomain: 'your-slack-team'
                )
            }
        }
    }
}

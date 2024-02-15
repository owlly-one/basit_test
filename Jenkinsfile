pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building stages..."
                script {
                    // Use 'nvm' to manage Node.js versions
                    // def nodejsInstallation = tool name: 'NodeJS', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
                    // env.PATH = "${nodejsInstallation}/bin:${env.PATH}"

                    // Install dependencies and build
                    sh 'npm install'
                }
            }
        }

        stage('Test') {
            steps {
                echo "Testing stages..."
                script {
                    // Run tests
                    sh 'npm test'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying..."
                script {
                    // Start the application
                    sh 'npm start'
                }
            }
        }
    }
}

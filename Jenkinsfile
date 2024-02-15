pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building stages..."
                script {
                    // Use 'nvm' to manage Node.js versions
                    def nodejsInstallation = tool name: 'nodejs', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
                    env.PATH = "${nodejsInstallation}/bin:${env.PATH}"

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
                    // Start the application (if needed)
                    sh 'npm run build'
                }
            }
        }

        stage('FTP Upload') {
            steps {
                script {
                    // Send build artifacts over FTP
                    ftpPublisher(
                        alwaysPublishFromMaster: false,
                        continueOnError: true,
                        failOnError: true,
                        publishers: [
                            [$class: 'FTPItem',
                             configName: 'ftpserver',
                             transfers: [
                                [$class: 'FTPTransfer',
                                 sourceFiles: 'build/**',
                                 remoteDirectory: '/']
                             ]
                            ]
                        ]
                    )
                }
            }
        }
    }
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
                continueOnError: true,
                failOnError: true,
                alwaysPublishFromMaster: false,
                masterNodeName: '',
                publishers: [
                    [$class: 'jenkins.plugins.publish_over_ftp.BapFtpPublisherPlugin', 
                     pluginInfo: [
                         configurationName: 'ftpserver',
                         transfers: [
                             [$class: 'jenkins.plugins.publish_over_ftp.Transfer', 
                              remoteDirectory: '/',
                              sourceFiles: 'build/**',
                              removePrefix: 'build']
                         ]
                     ]
                    ]
                ]
            )
        }
    }
}
    }
}
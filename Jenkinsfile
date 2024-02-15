pipeline {
  agent any

  stages {
    stage('Build and Deploy') {
      steps {
        echo "Building and deploying stages..."
        script {
          // Use 'nvm' to manage Node.js versions
          def nodejsInstallation = tool name: 'nodejs', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
          env.PATH = "${nodejsInstallation}/bin:${env.PATH}"

          // Install dependencies and build
          sh 'npm install'

          // Run tests (optional)
          // sh 'npm test' // Uncomment if you want to run tests

          // Build and start the application
          sh 'npm run build'
        }
      }
    }

    stage('FTP Upload') {
      steps {
        echo "Uploading artifacts to FTP server..."
        script {
          // Send build artifacts over FTP with error handling
          try {
            ftpPublisher(
              continueOnError: false, // Stop on errors
              failOnError: true,
              alwaysPublishFromMaster: false,
              masterNodeName: '',
              publishers: [
                [$class: 'BapFtpParamPublish',
                  configName: 'ftpserver', // Replace with your FTP server config name
                  transfers: [
                    [$class: 'BapFtpParamPublish',
                      remoteDirectory: '/', // Customize remote directory if needed
                      sourceFiles: 'build/**', // Customize source files pattern
                      removePrefix: 'build']
                  ]
                ]
              ]
            )
          } catch (error) {
            echo "Error uploading artifacts: ${error.message}"
            // Handle the error here, e.g., send notification, retry upload
          }
        }
      }
    }
  }
}

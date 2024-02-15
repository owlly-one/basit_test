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
            ftpPublisher(
                server: 'ftpserver', // Name of the configured server
                transfers: [
                 // Include files or directories with Ant-style patterns
                        remoteDirectory: '/',
                        sourceFiles: 'build/**',
                        removePrefix: 'build'
  ]
)
          
        }
      }
    }
  }
}

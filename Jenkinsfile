pipeline {
    agent any
    stages {
        steps{
            stage('build') {
                steps{
                    echo "building states..."
                    sh 'node -v'
                    sh 'npm install'
                }
            }
            stage('test') {
                steps{
                    echo "testing states..."
                    sh 'node test'
                }
        }
        stage('deploy') {
                steps{
                    echo "deploying"
                    sh 'npm start'
                }
    }
}
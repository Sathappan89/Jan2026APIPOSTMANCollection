pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building the war"
            }
        }

        stage('Deploy to QA') {
            steps {
                echo "Deploying to QA"
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Sathappan89/Jan2026APIPOSTMANCollection.git'
            }
        }

        stage('Pull Docker Image') {
            steps {
                sh 'docker pull sathappanas/gorestdatadriventesting:1.0'
            }
        }

        stage('Run API Test Cases') {
            steps {
                sh 'docker run -v $(pwd)/newman:/app/results sathappanas/gorestdatadriventesting:1.0'
            }
        }

        stage('Publish HTML Extra Report') {
            steps {
                publishHTML([
                    allowMissing: false,
                    alwaysLinkToLastBuild: false,
                    keepAll: true,
                    reportDir: 'newman',
                    reportFiles: 'gorest.html',
                    reportName: 'HTML Extra API Report',
                    reportTitles: ''
                ])
            }
        }

        stage('Deploy to PROD') {
            steps {
                echo "Deploying to PROD"
            }
        }
    }
}
pipeline {
    agent any

    environment {
        NEXUS_URL = 'http://your-nexus-repo-url' // Replace with your Nexus repository URL
        NEXUS_USERNAME = credentials('your-nexus-username-credential-id')
        NEXUS_PASSWORD = credentials('your-nexus-password-credential-id')
        GITHUB_REPO_URL = 'https://github.com/your-username/your-repo.git' // Replace with your GitHub repository URL
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Clone your GitHub repository
                    git url: GITHUB_REPO_URL
                }
            }
        }

        stage('Build and Package') {
            steps {
                script {
                    // Install any necessary Python dependencies
                    sh 'pip install -r requirements.txt'

                    // Create a ZIP archive of your Python project (main.py and other files)
                    sh 'zip -r my_python_app.zip .'
                }
            }
        }

        stage('Upload to Nexus') {
            steps {
                script {
                    // Define the filename of the ZIP archive
                    def artifactFileName = 'my_python_app.zip'

                    // Use curl to upload the ZIP archive to Nexus
                    sh "curl -u ${NEXUS_USERNAME}:${NEXUS_PASSWORD} --upload-file ${artifactFileName} ${NEXUS_URL}/your-repository-path/${artifactFileName}"
                }
            }
        }
    }
}

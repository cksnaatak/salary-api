pipeline {
    agent any

    environment {
        // Set the Maven path if needed
        MAVEN_HOME = '/usr/local/maven' // Adjust based on where Maven is installed
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout from the correct branch ('main' instead of 'master')
                git branch: 'main', 
                    url: 'https://github.com/cksnaatak/salary-api.git',
                    // credentialsId: 'your-credentials-id' // Replace with your actual credentials ID if repo is private
            }
        }
        
        stage('Build') {
            steps {
                script {
                    // Run Maven clean and install command to build the project
                    sh "'${MAVEN_HOME}/bin/mvn' clean install"
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Run Maven test to execute unit tests
                    sh "'${MAVEN_HOME}/bin/mvn' test"
                }
            }
        }

        stage('Publish Test Results') {
            steps {
                // Publish the test results (adjust the path if necessary)
                junit '**/target/test-*.xml'
            }
        }
    }

    post {
        always {
            // Archive artifacts (optional, you can adjust the path based on your project)
            archiveArtifacts '**/target/*.jar' // Adjust if your project creates a different artifact
        }
        success {
            // Actions to take when the build is successful
            echo 'Build and tests passed successfully!'
        }
        failure {
            // Actions to take when the build fails
            echo 'Build or tests failed!'
        }
    }
}

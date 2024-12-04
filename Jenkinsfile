pipeline {
    agent any

    environment {
        MAVEN_HOME = '/usr/local/maven' // Adjust if Maven is installed elsewhere
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the GitHub repository
                git 'https://github.com/cksnaatak/salary-api.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    // Run Maven to clean and build the project
                    sh "'${MAVEN_HOME}/bin/mvn' clean install"
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    // Run tests using Maven
                    sh "'${MAVEN_HOME}/bin/mvn' test"
                }
            }
        }
        stage('Publish Test Results') {
            steps {
                junit '**/target/test-*.xml'  // Jenkins JUnit plugin will read these results
            }
        }
    }
    post {
        always {
            // Archive the build artifacts (optional)
            archiveArtifacts '**/target/*.jar' // If applicable, adjust for your project
        }
        success {
            // Actions when the build is successful
            echo 'Build and tests passed!'
        }
        failure {
            // Actions when the build fails
            echo 'Build or tests failed!'
        }
    }
}

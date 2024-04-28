pipeline {
    agent {
        // Specifies the agent where the pipeline will run
        label 'Azure'
    }

    stages {
        stage('Install Apache') {
            steps {
                script {
                    // Update package repositories
                    sh 'sudo apt update'
                    // Install Apache web server
                    sh 'sudo apt install -y apache2'
                }
            }
        }

        stage('Check for errors') {
            steps {
                script {
                    // Define the directory containing Apache logs
                    def logDir = '/var/log/apache2'
                    // Execute grep command to find error files
                    def errorFiles = sh(script: "grep -lE '\\s(40[0-9]|50[0-9])\\s' $logDir/*.log", returnStdout: true).trim()
        
                    // Check if error files are found
                    if (!errorFiles.isEmpty()) {
                        // If error files are found, print an alert message
                        echo "Alert! Errors detected in Apache2 logs:"
                        // Print each error file found
                        errorFiles.readLines().each { file ->
                            echo file
                        }
                    } else {
                        // If no error files are found, print a message indicating no errors
                        echo "No errors found in Apache2 logs"
                    }
                }
            }
        }
    }
}

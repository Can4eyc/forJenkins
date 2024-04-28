pipeline {
    agent any

    stages {
        stage('Install Apache') {
            steps {
                script {
                    sh 'sudo apt update'
                    sh 'sudo apt install -y apache2'
                }
            }
        }

        stage('Check for errors') {
            steps {
                script {
                    def logDir = '/var/log/apache2'
                    def errorFiles = sh(script: "grep -lE '\\\\s(40[0-9]|50[0-9])\\\\s' $logDir/*.log", returnStdout: true).trim().split('\n')

                    if (errorFiles.size() > 0) {
                        echo "Alert! Errors detected in Apache2 logs:"
                        for (file in errorFiles) {
                            echo " - ${file}"
                        }
                    } else {
                        echo "No errors found in Apache2 logs"
                    }
                }
            }
        }
    }
}


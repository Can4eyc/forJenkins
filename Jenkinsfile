pipeline {
    agent {
        label 'Azure'
    }

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
                    def errorFiles = sh(script: "grep -lEq '\\s(40[0-9]|50[0-9])\\s' $logDir/*.log && echo 'Found'", returnStdout: true).trim()

                    if (errorFiles.contains('Found')) {
                        echo "Alert! Errors detected in Apache2 logs:"
                        sh "grep -lE '\\s(40[0-9]|50[0-9])\\s' $logDir/*.log"
                    } else {
                        echo "No errors found in Apache2 logs"
                    }
                }
            }
        }
    }
}

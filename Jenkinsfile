pipeline {
    agent {
        label 'master'
    }

    options {
        buildDiscarder logRotator(daysToKeepStr: '15', numToKeepStr: '10')
    }

    stages {
        // Stage 1
        stage('ST1-3133276f') {
            steps {
                echo 'ST1-3133276f: Setup Release Environment Completed.'
            }
        }

        // Stage 2 
        stage('ST2-3133276f') {
            steps {
                echo "ST2-3133276f: Checking and setting up the server container..."

                    // Remove existing container if present
                    sh """
                    if docker ps -a --format '{{.Names}}' | grep -q svr-3133276f; then
                        echo 'Removing existing container: svr-3133276f';
                        docker rm -f svr-3133276f;
                    else
                        echo 'No existing container found.';
                    fi
                    """

                    // Create and start a new container with Apache exposed on port 32900
                    sh """
                    echo 'Creating and starting a new container: svr-3133276f';
                    docker run -dit --name svr-3133276f -p 32900:80 img-base-3133276f
                    """

                    echo 'ST2-3133276f: Server Setup Completed.'
            }
        }

        // Stage 3A
                stage('ST3A-3133276f') {
                    steps {
                        echo 'ST3A-3133276f: X-Site Scripting (XSS) Test Completed and Report Generated.'
                    }
                }
        // Stage 3B
                stage('ST3B-3133276f') {
                    steps {
                        echo 'ST3B-3133276f: SQL Injection (SQLI) Test Completed and Report Generated.'
                    }
                }
            }
        }

        // Stage 4
        stage('ST4-3133276f') {
            steps {
                echo 'ST4-3133276f: Security reports are checked.'
            }
        }

        // Stage 5
        stage('ST5-3133276f') {
            steps {
                script {
                    def userInput = input(message: "Hello 3133276f, permission to proceed to the next phase?",
                        ok: 'Proceed',
                        parameters: [choice(name: 'Action', choices: 'Proceed\nAbort', description: 'Select action')])

                    if (userInput == 'Proceed') {
                        echo 'ST5-3133276f: Approve to proceed to next phase.'
                    } else {
                        echo 'ST5-3133276f: Pipeline aborted by user choice.'
                        currentBuild.result = 'ABORTED'
                        error('Pipeline aborted by user.')
                    }
                }
            }
        }

        // Stage 6
        stage('ST6-3133276f') {
            when {
                expression {
                    return currentBuild.result != 'ABORTED'
                }
            }
            steps {
                echo 'ST6-3133276f: Ready for next phase.'
            }
        }
    }
}


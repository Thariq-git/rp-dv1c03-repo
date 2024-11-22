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
                script {
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
                    docker run -d -it --name svr-3133276f -p 32900:80 img-base-3133276f /bin/sh -c "apachectl -D FOREGROUND"
                    """

                    echo 'ST2-3133276f: Server Setup Completed.'
                }
            }
        }

        // Additional stages can be added here
    }
}

pipeline {
    agent any

    environment {
        PROJECT_DIR = "/var/jenkins_home/workspace/hphhealthcare/hphhealthcare/hphhealth" // Full path to the project directory
        DOCKER_IMAGE = "hcmuleva/hphhealthcare" // Replace with your Docker image name
    }

    stages {
        stage('Git Pull') {
            steps {
                script {
                    echo 'Pulling the latest changes from Git...'
                    sh """
                    cd ${PROJECT_DIR}
                    git fetch origin
                    git reset --hard origin/main
                    """
                }
            }
        }
        stage('Build Maven Project') {
            steps {
                script {
                    echo 'Building the Maven project...'
                    sh """
                    cd ${PROJECT_DIR}
                    mvn clean install
                    """
                }
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    echo 'Building the Docker image...'
                    sh """
                    cd ${PROJECT_DIR}
                    docker build -t ${DOCKER_IMAGE}:latest .
                    """
                }
            }
        }
    }
}

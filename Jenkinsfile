pipeline {
    agent any

    environment {
        PROJECT_DIR = "/var/lib/jenkins/workspace/hphpipeline_main/sourcecode/hphhealthcare/hphhealth" // Full path to the project directory
        DOCKER_IMAGE = "hcmuleva/hphhealthcare" // Replace with your Docker image name
    }

    stages {
        stage('Git Pull') {
            steps {
                script {
                    echo 'Pulling the latest changes from Git git pull... changed for webhook configured and testing'
                   
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

pipeline {
    agent any

    environment {
        PROJECT_DIR = "hphhealthcare" // Directory of your project
        DOCKER_IMAGE = "healthcare" // Replace with your Docker image name
    }

    stages {
        stage('Git Pull') {
            steps {
                script {
                    echo 'Checking for changes in the repository...'
                    echo ' $(env.PROJECT_DIR) director'
                    dir(env.PROJECT_DIR) {
                        // Fetch and check for changes
                        sh """
                        git fetch origin
                        git reset --hard origin/main
                        """
                    }
                }
            }
        }
        stage('Build Maven Project') {
            steps {
                script {
                    echo 'Building Maven Project...'
                    dir(env.PROJECT_DIR) {
                        // Run Maven build
                        sh 'mvn clean install'
                    }
                }
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    echo 'Building Docker image...'
                    dir(env.PROJECT_DIR) {
                        sh "docker build -t ${DOCKER_IMAGE}:latest ."
                    }
                }
            }
        }
    }
}

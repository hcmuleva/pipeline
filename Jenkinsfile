pipeline {
    agent any

    environment {
        PROJECT_DIR = "/var/lib/jenkins/workspace/hphpipelie/hphhealthcare/hphhealth"

        DOCKER_IMAGE = "hcmuleva/hphhealthcare" // Replace with your Docker image name
    }

    stages {
        stage('Git Pull') {
            steps {
                script {
                    echo 'Pulling the latest changes from Git git pull... changed for webhook configured'
                   
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
                    mvn clean test
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
            post {
                always {
                    jacoco(
                        execPattern: 'target/*.exec',
                        classPattern: 'target/classes',
                        sourcePattern: 'src/main/java',
                        exclusionPattern: 'src/test/*'
                    )
                }
            }
        }
        
    }
}

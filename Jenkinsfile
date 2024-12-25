pipeline {
    agent any
    environment {
        PROJECT_DIR = "/var/lib/jenkins/workspace/hphpipelie/hphhealthcare/hphhealth"
        DOCKER_IMAGE = "hcmuleva/hphhealthcare"
    }
    
    stages {
        stage('Git Pull') {
            steps {
                echo 'Pulling the latest changes from Git git pull... changed for webhook configured'
            }
        }
        
        stage('Build Maven Project') {
            steps {
                sh """
                    cd ${PROJECT_DIR}
                    mvn clean package
                    mvn test
                    ls -l target/hphhealth-1.0-SNAPSHOT.jar
                """
            }
        }

        stage('Code Coverage') {
            steps {
                recordCoverage(
                    tools: [[parser: 'JACOCO']],
                    sourceDirectories: [[path: "${PROJECT_DIR}/src/main/java"]],
                    reportFiles: [[path: "${PROJECT_DIR}/target/site/jacoco/jacoco.xml"]]
                )
            }
        }
        
        stage('Docker Build') {
            steps {
                sh """
                    cd ${PROJECT_DIR}
                    pwd
                    ls -la
                    ls -la target/
                    docker build -t ${DOCKER_IMAGE}:latest .
                """
            }
        }
    }
}

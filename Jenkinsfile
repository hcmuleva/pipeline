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
                withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
                sh """
                    cd ${PROJECT_DIR}
                    mvn clean package
                    mvn test
                    mvn clean install sonar:sonar -Dsonar.login=${SONAR_TOKEN}
                """
        }
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

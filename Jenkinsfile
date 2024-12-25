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
                mvn clean package -DskipTests    # First build the JAR
                mvn test                         # Then run tests
            """
            
            // Verify JAR exists
            sh """
                cd ${PROJECT_DIR}
                ls -l target/hphhealth-1.0-SNAPSHOT.jar
            """
        }
    }
    post {
        always {
            jacoco(
                execPattern: '${PROJECT_DIR}/target/*.exec',
                classPattern: '${PROJECT_DIR}/target/classes',
                sourcePattern: '${PROJECT_DIR}/src/main/java',
                exclusionPattern: '${PROJECT_DIR}/src/test/*'
            )
        }
    }
}

stage('Docker Build') {
    steps {
        script {
            echo 'Building the Docker image...'
            sh """
                cd ${PROJECT_DIR}
                # Print directory contents for debugging
                pwd
                ls -la
                ls -la target/
                
                # Build Docker image
                docker build -t ${DOCKER_IMAGE}:latest .
            """
        }
    }
}
        
    }
}

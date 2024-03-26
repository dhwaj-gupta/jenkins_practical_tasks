pipeline {
    agent any
    
    stages {
        stage('Checkstyle') {
            steps {
                // Assuming you're using Maven for checkstyle
                sh 'mvn checkstyle:checkstyle'
                archiveArtifacts artifacts: '**/checkstyle-result.xml', fingerprint: true
            }
        }
        stage('Test') {
            steps {
                // Assuming you're using Maven for running tests
                sh 'mvn test'
            }
        }
        stage('Build') {
            steps {
                // Assuming you're using Maven for building the application
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Create Docker Image for MR') {
            steps {
                // Assuming Dockerfile is present in the repository root directory
                sh 'docker build -t myapp:${GIT_COMMIT:0:7} .'
                sh 'docker tag myapp:${GIT_COMMIT:0:7} <your_registry_url>/mr:latest'
                sh 'docker push <your_registry_url>/mr:latest'
            }
        }
    }
}



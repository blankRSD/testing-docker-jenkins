pipeline {
    agent any
    tools {
        maven "maven"
    }
    stages {
        stage('Install') {
            steps {
                echo "Installing..."
                git 'https://github.com/blankRSD/testing-docker-jenkins.git'
                sh "mvn -Dmaven.test.failure.ignore=true clean install"
            }
        }
        stage('Build') {
            steps {
                echo "Building..."
                sh "docker image build -t test-docker-jenkins ."
            }
        }
        stage('Deployment') {
            steps {
                echo "Deploying..."
                sh "docker run test-docker-jenkins"
            }
        }
        
    }
    post {
        failure {
		    echo "Application failed" 
        }
    }    
}

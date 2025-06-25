pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'hello-world-python:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Kishan-Prakash/jenkins_docker_python_hello_world.git'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    if (fileExists('Dockerfile')) {
                        sh 'docker build -t ${env.DOCKER_IMAGE} .'
                    } else {
                        error 'Dockerfile not found in the workspace. Please ensure it exists.'
                    }
                }
            }
        }

        stage('Docker Run (Optional)') {
            steps {
                sh "docker run --rm ${env.DOCKER_IMAGE}"
            }
        }
    }

    post{
        success {
            echo 'Python application Docker image built successfully!'
        }
        failure {
            echo 'There was an error building the Docker image.'
        }
    }
}


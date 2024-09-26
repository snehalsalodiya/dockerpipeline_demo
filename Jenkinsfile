pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS = credentials('docker')  // Using 'docker' as the credentials ID
    }

    stages {
        stage("Checkout") {
            steps {
                git branch: 'main', url: 'https://github.com/snehalsalodiya/dockerpipeline_demo', credentialsId: 'github'
            }
        }
        stage("Build Image") {
            steps {
                script {
                    sh 'docker --version' // Check if Docker is available
                    sh 'docker build -t snehalsalodiya/dockerpipeline .'
                }
            }
        }
        stage('Docker Push') {
            steps {
                script {
                    // Login to Docker Hub
                    if (isUnix()) {
                        sh "echo ${DOCKER_CREDENTIALS_PSW} | docker login -u ${DOCKER_CREDENTIALS_USR} --password-stdin"
                        sh 'docker push snehalsalodiya/dockerpipeline'
                        sh 'docker logout'
                    } else {
                        bat "echo %DOCKER_CREDENTIALS_PSW% | docker login -u %DOCKER_CREDENTIALS_USR% --password-stdin"
                        bat 'docker push snehalsalodiya/dockerpipeline'
                        bat 'docker logout'
                    }
                }
            }
        }
    }
}

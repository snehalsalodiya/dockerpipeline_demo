pipeline {
    agent any

    stages {
        stage("Checkout") {
            steps {
                git branch: 'main', url: 'https://github.com/snehalsalodiya/dockerpipeline_demo'
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
        stage("Docker Push") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                    sh 'docker push snehalsalodiya/dockerpipeline'
                    sh 'docker logout'
                }
            }
        }
    }
}

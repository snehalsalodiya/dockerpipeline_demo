pipeline {
    agent any

    stages {
        stage("Checkout") {
            steps {
                git branch: 'main', url: 'https://github.com/snehalsalodiya/dockerpipeline_demo',credentialsId: 'github'
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
                
                    def username = 'snehalsalodiya'
                    def password = 'snehal@7850' 

                    if (isUnix()) {
                        sh "echo ${password} | docker login -u ${username} --password-stdin"
                        sh 'docker push snehalsalodiya/dockerpipeline'
                        sh 'docker logout'
                    } else {
                        bat "echo %password% | docker login -u %username% --password-stdin"
                        bat 'docker push snehalsalodiya/dockerpipeline'
                        bat 'docker logout'
                    }
                }
            }
        }
    }
}

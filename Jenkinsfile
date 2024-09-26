pipeline {
    agent any

    stages {
        stage("Checkout") {
            steps {
                git branch: 'main', url: 'git@github.com/snehalsalodiya/dockerpipeline_demo'
            }
        }
        stage("Build Image") {
            steps {
                script {
                    if (isUnix()) {
                        sh 'docker build -t snehalsalodiya/dockerpipeline .'
                    } else {
                        bat 'docker build -t snehalsalodiya/dockerpipeline .'
                    }
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
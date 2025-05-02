pipeline {
    agent any

    environment {
        IMAGE_NAME = "12kishor/sample-react-app"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/kish-1/jenu-1.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t ${IMAGE_NAME} .'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-cred', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    script {
                        sh """
                            echo \$PASSWORD | docker login -u \$USERNAME --password-stdin
                            docker push ${IMAGE_NAME}
                        """
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline finished successfully 🎉'
        }
        failure {
            echo 'Something went wrong 💥'
        }
    }
}


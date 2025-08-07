pipeline {
    agent {
        docker {
            image 'node:18'
        }
    }

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    dockerImage = docker.build("jenkins-node-app")
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker run -d -p 3000:3000 --name node-app jenkins-node-app || true'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution complete.'
        }
    }
}

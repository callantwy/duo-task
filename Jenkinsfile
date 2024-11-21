pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
                docker build -t callantwy/myflaskapp:latest -t callantwy/myflaskapp:v${BUILD_NUMBER} .
                '''
            }
        }
        stage('Push') {
            steps {
                sh '''
                docker push callantwy/myflaskapp:latest
                docker push callantwy/myflaskapp:v${BUILD_NUMBER}
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh'''
                kubectl apply -f .
                kubectl set image deployment/flask flask-container=callantwy/myflaskapp:v${BUILD_NUMBER}
                '''
            }
        }
    }
}

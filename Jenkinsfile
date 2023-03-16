pipeline {
    agent any
    stages {
        stage ('Lint HTML') {
            steps {
                sh 'tidy -q -e *.html'
            }
        }
        stage ('Upload to AWS') {
            steps {
                withAWS(region: 'ap-south-1', credentials: 'aws-id') {
                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'index.html', bucket: 'jenkins-project-final')
                }
            }
        }
    }
}
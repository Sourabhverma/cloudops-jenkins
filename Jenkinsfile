pipeline {
    agent any
    stages {
        stage ('Lint HTML') {
            steps {
                sh 'tidy -q -e *.html'
            }
        }
        stage('Unit Test') {
             steps {
                 sh 'echo "Fail!"; exit 1'
             }
         }

        stage ('Upload to AWS') {
            steps {
                withAWS(region: 'us-west-2', credentials: 'aws-id') {
                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'index.html', bucket: 'jenkins-project-final')
                }
            }
        }
    }
        post {
             always {
                 mail bcc: '', body: "<b>Example</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: "sourabhvverma@gmail.com";
             }
        }
}
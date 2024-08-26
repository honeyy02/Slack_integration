pipeline {
    agent any

    environment {
        SLACK_CHANNEL = '#demo-channel'
        SLACK_CREDENTIAL_ID = 'slack-bot-token'
    }

    stages {
        stage('Compile') {
            steps {
                echo 'Compiling...'
                sh 'javac Main.java'
            }
        }
      stage('Run') {
            steps {
                echo 'Running...'
                sh 'java Main'
            }
        }
    }

    post {
        success {
            slackSend (
                channel: "${env.SLACK_CHANNEL}",
                color: 'good',
                message: "Build successful! Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})"
            )
        }
        failure {
            slackSend (
                channel: "${env.SLACK_CHANNEL}",
                color: 'danger',
                message: "Build failed! Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})"
            )
        }
    }
}

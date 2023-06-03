pipeline {
    agent {node {label 'qa'}}
    stages {
        stage('Build development') {
            steps {
                sh 'composer install'
            }
        }
        stage('teste') {
            steps {
                sh 'vendor/bin/phpunit'
            }
        }       
    }
    post {
        failure {
            emailtext(
                subject: "Job '${env.JOB_NAME} ${env.BUILD_NUMBER}'"
                body: "Job deu ruim '${env.JOB_NAME} ${env.BUILD_NUMBER}'"
                recipientProviders: [[$class: 'DevelopersRecipientProvider'],
                [$class: 'RequestRecipientProvider']]
            )
        success {
            emailtext(
                subject: "Job '${env.JOB_NAME} ${env.BUILD_NUMBER}'"
                body: "Sucess o no Job '${env.JOB_NAME} ${env.BUILD_NUMBER}'"
                to: "danpayne21@gmail.com"
            )
        }
    }
}

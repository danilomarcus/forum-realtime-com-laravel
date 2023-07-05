pipeline {
    agent none
    stages {
        stage('Build development') {
            agent {node {label 'qa'}}
            steps {
                sh 'composer install'
            }
        }
        stage('configurar servidor por ansible') {
            agent {node {label 'master'}}
            steps {
                sh 'ansible-playbook /home/ubuntu/laravel/mysql.yaml -i /home/ubuntu/laravel/mysql'
            }
        }  
        stage('teste') {
            agent {node {label 'qa'}}
            steps {
                sh 'vendor/bin/phpunit'
            }
        }       
    }
    post {
        failure {
            emailext(
                subject: "Job '${env.JOB_NAME} ${env.BUILD_NUMBER}'",
                body: """<p>A Build Falhou <a href="${env.BUILD_URL}">${env.JOB_NAME}</a></p>""",
                recipientProviders: [[$class: 'DevelopersRecipientProvider'],
                [$class: 'RequesterRecipientProvider']]
            )
        }
        success {
            emailext(
                subject: "Job '${env.JOB_NAME} ${env.BUILD_NUMBER}'",
                body: "Sucesso no Job '${env.JOB_NAME} ${env.BUILD_NUMBER}'",
                to: "danpayne21@gmail.com"
            )
        }
    }
}

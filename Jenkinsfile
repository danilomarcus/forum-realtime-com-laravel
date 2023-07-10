pipeline {
    agent none
    stages {
        stage('Build development') {
            agent {node {label 'qa2'}}
            steps {
                sh 'composer install'
                sh 'rm index.nginx-debian.html'
            }
        }
        stage('Pre-teste banco Mysql') {
            agent {node {label 'qa2'}}
            steps {
                sh 'ansible-playbook /home/ubuntu/laravel/mysql.yaml -i /home/ubuntu/laravel/mysql'
            }
        }
        stage('Testes automatizados') {
            agent {node {label 'qa2'}}
            steps {
                sh 'echo "testando..."'
            }
        }
        stage('Deploy') {
            agent {node {label 'qa2'}}
            when {
                branch 'develop'
            }
            steps {
                sh 'ansible-playbook /home/ubuntu/laravel/playbook.yml'
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

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
}

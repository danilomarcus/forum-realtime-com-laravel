pipeline {
    agent {node {label 'qa'}}
    stages {
        stage('Build development') {
            when {
                branch 'develop'
            }
            steps {
                sh 'composer install'
            }
        }        
    }
}

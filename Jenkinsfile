pipeline {
    agent {
        docker {
            label 'remote_builder'
            image 'maven:3-alpine'
        }
    }
    stages {
        stage('build') { 
            steps {
                sh 'mvn --version'
                sh 'ls -l'
            }
        }
    }
}
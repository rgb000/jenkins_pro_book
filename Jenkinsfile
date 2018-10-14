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
                sh 'pwd'
		sh 'ls -l'
            }
        }
    }
}

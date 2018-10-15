node('remote_builder') {
    withDockerContainer(args: '-u 0', image: 'maven:3-alpine') {
        stage('scm') {
            checkout([$class: 'GitSCM', branches: [[name: ':origin/feature-\\d+']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'PreBuildMerge', options: [mergeRemote: 'origin', mergeTarget: 'master']]], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'sysops', url: 'https://github.com/rgb000/jenkins_pro_book.git']]])
        }
        stage('build') {
            dir('hello-world-greeting') {
                sh 'mvn clean install'
            }
        }
        stage('git install') {
            sh 'apk update && apk add git'
        }
        stage('push') {
            sh 'git config --global user.email "rgb000@jprotest.com"'
            sh 'git config --global user.name "rgb000"'
            sh("git tag -a ${BUILD_NUMBER} -m 'Jenkins'")
            withCredentials([string(credentialsId: '6c658de6-0444-4051-aa41-8bb76cd3ceda', variable: 'credent')]) {
                sh("git push https://${credent}@github.com/rgb000/jenkins_pro_book.git HEAD:master --tags")
            }
        }
    }
}

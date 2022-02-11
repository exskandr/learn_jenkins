#!groovy
// Run docker build
properties([disableConcurrentBuilds()])

pipeline {
    agent {
        any
        }
    triggers { pollSCM('* * * * *') }
    options {
        buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10'))
        timestamps()
    }
    stages {
        stage("create docker image") {
            steps {
                echo " ============== start building image =================="
                dir ('docker/toolbox') {
                	sh 'docker build -t exskandr/toolbox:latest . '
                }
            }
        }
        stage("docker push") {
            steps {
                echo " ============== start pushing image =================="
                sh '''
                docker push exskandr/toolbox:latest
                '''
            }
        }
    }
}
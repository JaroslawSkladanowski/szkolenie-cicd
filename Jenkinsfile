pipeline {

    tools {
        maven 'maven-3'
    }
    agent any
    stages {
        stage('Clean') {
            steps {
                cleanWs()
            }
        }
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/JaroslawSkladanowski/szkolenie-cicd-jenkins-gitlab-example.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'

            }
        }
    }
    post {
        always {
            junit allowEmptyResults: true, testResults: '**/target/**/TEST-*.xml'
            slackSend channel: 'jenkins-jarek-skladanowski', message: "Build started - ${env.BUILD_TAG}(<${env.BUILD_URL}|Open>)"
        }
    }
}
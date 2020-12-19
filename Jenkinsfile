pipeline {
    options {
        disableConcurrentBuilds()
    }
    
    agent any

    environment {
        BUILD_URL = "${BUILD_URL}"
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building project...'
                sh 'ls'
                sh 'cd maven-code-coverage'
                sh 'mvn install'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy project...'
            }
        }
        }
        post {
            always {
                influxDbPublisher(selectedTarget: 'TestDB', customData: assignURL(BUILD_URL))
            }
        }
    }

def assignURL(build_url) {
    def buildURL = [:]
    buildURL['url'] = build_url
    return buildURL
}

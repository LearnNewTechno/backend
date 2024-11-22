pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 30, unit: 'MINUTES') 
        disableConcurrentBuilds()
        retry(2)
    }
    environment {
        appVersion = '' // this will become global, we can use accross the pipeline
    }
    
    stages {
        stage('Read the version') {
            steps {
                script {
                    def packagejson = readJSON file: 'package.json'
                    appVersion = packagejson.version
                    echo "App version: ${appVersion}"
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Docker Build') {
            steps {
                sh """
                    docker build -t saanvilikhith/backend:${appVersion} .
                    docker images
                """ 
            }
        }
        
    }
    post {
        always {
            echo "this sections runs always"
            deleteDir()
        }
        success {
            echo "this section run when success"
        }
        failure {
             echo "this section run when failure"
             
        }
    } 
}
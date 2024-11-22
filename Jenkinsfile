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
        stage('Build') {
            steps {
                sh 'echo this is build'  
                // sh 'sleep 10'
            }
        }
        stage('Test') {
            steps {
                sh 'echo this is Test'  
                sh 'env'
            }
        }
        stage('Deploy') {
            when {
                expression {env.GIT_BRANCH == 'origin/main'}
            }
            steps {
                sh 'echo this is Deploy' 
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
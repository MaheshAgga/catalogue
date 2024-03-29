pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }
    environment {
        packageVersion = ''
    }
    stages {
        stage('Get the version') {
            steps {
                script{
                def packageJson= readJSON file: 'package.json'
                packageVersion= packageJson.version
                echo "app version is:$packageVersion"
                }
            }
        }
        stage('install  dependencies'){
            steps{
                sh """
                    npm install
                """
            }
        }
        stage('Build..') {
            steps {
                sh """
                ls -la
                zip -q -r catalogue.zip ./* -x ".git" -x "*.zip"
            """
            }
        }
        stage ('Testing') {
           steps {
            echo 'Testing...'
           }
        }
        stage ('Deploy') {
            steps {
                echo 'Deploy...'
            }
        }
    }
    //post build
    post {
        always {
            echo 'I will always says HareKrishna HareRama......'
            deleteDir()
        }
        failure{
            echo 'failure'
        }
        success{
            echo 'success'
        }
    }
}

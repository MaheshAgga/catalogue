pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }
     environment { 
        packageVersion = ''
        nexusURL = '172.31.83.247:8081'
    }
    options {
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()
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
                ls -ltr
            """
            }
        }
        stage('publish artifact'){
            steps {
                
                nexusArtifactUploader(
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        nexusUrl: "${nexusURL}",
                        groupId: 'com.roboshop',
                        version: "${packageVersion}",
                        repository: 'catalogue',
                        credentialsId: 'nexus-auth',
                        artifacts: [
                            [artifactId: catalogue,
                            classifier: '',
                            file: 'catalogue.zip',
                            type: 'zip']
                    ]
                )
                
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

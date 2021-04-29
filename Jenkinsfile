pipeline {
    environment {
        DOTNET_CLI_HOME = "/tmp/dotnet_cli_home"
    }
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('DotNet Build') {
            agent {
                docker { 
                    image 'mcr.microsoft.com/dotnet/sdk:5.0'
                    reuseNode true
                }
            }
            steps{
                script {
                    sh 'dotnet build'
                }
            }
        }
        stage('DotNet Test') {
            agent {
                docker { 
                    image 'mcr.microsoft.com/dotnet/sdk:5.0'
                    reuseNode true
                }
            }
            steps{
                script {
                    sh 'dotnet test'
                }
            }
        }
        stage ('NPM') {
            agent {
                docker { 
                    image 'node:14-alpine'
                    reuseNode true
                }
            }
            stages {
                stage('NPM Install') {
                    steps{
                        script {
                            dir("DotnetTemplate.Web") {
                                sh 'npm install'
                            }
                        }
                    }
                }
                stage('NPM Build') {
                    steps{
                        script {
                            dir("DotnetTemplate.Web") {
                                sh 'npm run build'
                            }
                        }
                    }
                }
                stage('NPM Test') {
                    steps{
                        script {
                            dir("DotnetTemplate.Web") {
                                sh 'npm t'
                            }
                        }
                    }
                }
                stage('NPM Lint') {
                    steps{
                        script {
                            dir("DotnetTemplate.Web") {
                                sh 'npm run lint'
                            }
                        }
                    }
                }
            }
        }
        
    }
}
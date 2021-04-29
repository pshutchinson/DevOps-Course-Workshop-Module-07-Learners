pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('DotNet Build') {
            agent {
                docker { image 'mcr.microsoft.com/dotnet/sdk:5.0'}
            }
            steps{
                script {
                    sh 'dotnet build'
                }
            }
        }
        stage('DotNet Test') {
            agent {
                docker { image 'mcr.microsoft.com/dotnet/sdk:5.0'}
            }
            steps{
                script {
                    sh 'dotnet test'
                }
            }
        }
        stage('NPM Install') {
            agent {
                docker { image 'node:14-alpine'}
            }
            steps{
                script {
                    sh 'cd DotnetTemplate.Web'
                    sh 'npm install'
                }
            }
        }
        stage('NPM Build') {
            agent {
                docker { image 'node:14-alpine'}
            }
            steps{
                script {
                    sh 'cd DotnetTemplate.Web'
                    sh 'npm run build'
                }
            }
        }
        stage('NPM Test') {
            agent {
                docker { image 'node:14-alpine'}
            }
            steps{
                script {
                    sh 'cd DotnetTemplate.Web'
                    sh 'npm t'
                }
            }
        }
        stage('NPM Lint') {
            agent {
                docker { image 'node:14-alpine'}
            }
            steps{
                script {
                    sh 'cd DotnetTemplate.Web'
                    sh 'npm run lint'
                }
            }
        }
    }
}
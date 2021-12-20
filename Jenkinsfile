pipeline {

    agent any

    environment {
        DEPLOY_CREDS = credentials('anypoint-creds')
        PLATFORM_CREDS = credentials('anypoint-platform-creds')
        MULE_VERSION = '4.3.0'
        BG = "Mulesoft"
        WORKER = '1'
        WORKERTYPE = 'MICRO'
        REGION = 'ap-southeast-2'
        API_NAME = 'helloworld'
    }

    stages {
        
        stage('Build'){
            steps {
                echo 'Building .....'
                echo env.GIT_BRANCH
            }
        }
        stage('Deploying in DEV'){
            when {
                branch "develop"
            }
            steps {
                echo 'Deploying in DEV'
            }
        }
        /*stage('Approve deployment on Test') {
            steps {
                timeout(time: 14, unit: 'DAYS') {
                    script {
                        env.DEPLOY_TEST = input message: 'Approve deployment on TEST', parameters: [
                        [$class: 'BooleanParameterDefinition', defaultValue: false, description: '', name: 'Approve deployment on TEST']
                        ]
                    }
                }
            }
        }*/
        stage('Deploying in TST'){
            when {
                branch "test"
            }
            steps {
                echo 'Deploying in TST'
            }
        }
        stage('Deploying in PROD'){
            when {
                anyOf{
                    branch "origin/master"
                    branch "origin/hotfix"
                    branch "origin/release"
                }
            }
            steps {
                echo 'Deploying in PROD'
            }
        }
    }


    tools {
        maven 'M3'
    }
}
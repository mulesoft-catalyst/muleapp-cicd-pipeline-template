pipeline {

    agent any

    environment {
        DEPLOY_CREDS = credentials('anypoint-creds')
        PLATFORM_CREDS = credentials('anypoint-platform-creds')
        MVN_SET = credentials('mule-settings')
        SECRET_KEY = credentials('secret-key')
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
                echo env.SECRET_KEY
                /*sh 'mvn -s $MVN_SET help:effective-settings'*/
            }
        }
        stage('Deploying in DEV'){
            when {
                branch "develop"
            }
            environment {
                ENVIRONMENT = 'DEV'
                DEPLOY_APP_NAME = 'app-dev'
                MULEENV = 'dev'
            }
            steps {
                echo 'Deploying in DEV'
                sh 'cat samplefile.txt'

                /*sh 'mvn -DskipTests deploy -DmuleDeploy -Dmule.version="$MULE_VERSION" -Danypoint.username="$DEPLOY_CREDS_USR" -Danypoint.password="$DEPLOY_CREDS_PSW" -Dcloudhub.app="$DEPLOY_APP_NAME" -Dcloudhub.environment="$ENVIRONMENT" -Dcloudhub.bg="$BG" -Dcloudhub.worker="$WORKER" -Dcloudhub.workerType="$WORKERTYPE" -Dmule.env="$MULEENV" -Denc.key="$SECRET_KEY" -Dcloudhub.region="$REGION" -Danypoint.platform.client_id="$PLATFORM_CREDS_USR" -Danypoint.platform.client_secret="$PLATFORM_CREDS_PSW"*/
            }
        }
        stage('Approve deployment on Test') {
            when {
                branch "develop"
            }
            steps {
                timeout(time: 14, unit: 'DAYS') {
                    script {
                        env.DEPLOY_TEST = input message: 'Approve deployment on TEST', parameters: [
                        [$class: 'BooleanParameterDefinition', defaultValue: false, description: '', name: 'Approve deployment on TEST']
                        ]
                    }
                }
            }
        }
        stage('Deploying in TST'){
            when {
                environment name: 'DEPLOY_TEST', value: "true"
            }
            environment {
                ENVIRONMENT = 'TEST'
                DEPLOY_APP_NAME = 'app-test'
                MULEENV = 'test'
            }
            steps {
                echo 'Deploying in TST'
                sh 'cat samplefile.txt'

                /*sh 'mvn -DskipTests deploy -DmuleDeploy -Dmule.version="$MULE_VERSION" -Danypoint.username="$DEPLOY_CREDS_USR" -Danypoint.password="$DEPLOY_CREDS_PSW" -Dcloudhub.app="$DEPLOY_APP_NAME" -Dcloudhub.environment="$ENVIRONMENT" -Dcloudhub.bg="$BG" -Dcloudhub.worker="$WORKER" -Dcloudhub.workerType="$WORKERTYPE" -Dmule.env="$MULEENV" -Denc.key="$SECRET_KEY" -Dcloudhub.region="$REGION" -Danypoint.platform.client_id="$PLATFORM_CREDS_USR" -Danypoint.platform.client_secret="$PLATFORM_CREDS_PSW"*/
            }
        }
        stage('Approve deployment on UAT') {
            steps {
                timeout(time: 14, unit: 'DAYS') {
                    script {
                        env.DEPLOY_UAT = input message: 'Approve deployment on UAT', parameters: [
                        [$class: 'BooleanParameterDefinition', defaultValue: false, description: '', name: 'Approve deployment on UAT']
                        ]
                    }
                }
            }
        }
        stage('Deploying in UAT'){
            when {
                anyOf{
                    environment name: 'DEPLOY_UAT', value: "true"
                    branch pattern: "hotfix\\/bug-\\d{1,}/gm" , comparator: "REGEXP"
                }
            }
            environment {
                ENVIRONMENT = 'UAT'
                DEPLOY_APP_NAME = 'app-uat'
                MULEENV = 'uat'
            }
            steps {
                echo 'Deploying in UAT'
                sh 'cat samplefile.txt'

                /*sh 'mvn -DskipTests deploy -DmuleDeploy -Dmule.version="$MULE_VERSION" -Danypoint.username="$DEPLOY_CREDS_USR" -Danypoint.password="$DEPLOY_CREDS_PSW" -Dcloudhub.app="$DEPLOY_APP_NAME" -Dcloudhub.environment="$ENVIRONMENT" -Dcloudhub.bg="$BG" -Dcloudhub.worker="$WORKER" -Dcloudhub.workerType="$WORKERTYPE" -Dmule.env="$MULEENV" -Denc.key="$SECRET_KEY" -Dcloudhub.region="$REGION" -Danypoint.platform.client_id="$PLATFORM_CREDS_USR" -Danypoint.platform.client_secret="$PLATFORM_CREDS_PSW"*/
            }
        }
        stage('Approve deployment on PROD') {
            steps {
                timeout(time: 14, unit: 'DAYS') {
                    script {
                        env.DEPLOY_PROD = input message: 'Approve deployment on PROD', parameters: [
                        [$class: 'BooleanParameterDefinition', defaultValue: false, description: '', name: 'Approve deployment on PROD']
                        ]
                    }
                }
            }
        }
        stage('Deploying in PROD'){
            when {
                environment name: 'DEPLOY_PROD', value: "true"
            }
            environment {
                ENVIRONMENT = 'PRD'
                DEPLOY_APP_NAME = 'app'
                MULEENV = 'prd'
            }
            steps {
                echo 'Deploying in PROD'

                /*sh 'mvn -DskipTests deploy -DmuleDeploy -Dmule.version="$MULE_VERSION" -Danypoint.username="$DEPLOY_CREDS_USR" -Danypoint.password="$DEPLOY_CREDS_PSW" -Dcloudhub.app="$DEPLOY_APP_NAME" -Dcloudhub.environment="$ENVIRONMENT" -Dcloudhub.bg="$BG" -Dcloudhub.worker="$WORKER" -Dcloudhub.workerType="$WORKERTYPE" -Dmule.env="$MULEENV" -Denc.key="$SECRET_KEY" -Dcloudhub.region="$REGION" -Danypoint.platform.client_id="$PLATFORM_CREDS_USR" -Danypoint.platform.client_secret="$PLATFORM_CREDS_PSW"*/
            }
        }
    }


    tools {
        maven 'M3'
    }
}
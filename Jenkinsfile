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


    tools {
        maven 'M3'
    }
}
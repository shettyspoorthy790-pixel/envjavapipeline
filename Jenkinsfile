pipeline {
    agent { label 'Testslave1' }

    parameters {
        choice(
            name: 'ENV',
            choices: ['dev', 'prod'],
            description: 'Select environment'
        )
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Compile') {
            steps {
                sh 'javac NumberCheck.java'
            }
        }

        stage('Run - DEV') {
            when {
                expression { params.ENV == 'dev' }
            }
            steps {
                echo 'Running in DEV environment'
                sh 'java NumberCheck'
            }
        }

        stage('Run - PROD') {
            when {
                expression { params.ENV == 'prod' }
            }
            steps {
                echo 'Running in PROD environment'
                sh 'java NumberCheck'
            }
        }
    }
}

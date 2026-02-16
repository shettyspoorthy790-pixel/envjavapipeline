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
                sh '''
                echo "Files in workspace:"
                ls -l
                javac NumberCheck.java
                '''
            }
        }

        stage('Run - DEV') {
            when {
                expression { params.ENV == 'dev' }
            }
            steps {
                sh '''
                echo "Running in DEV environment"
                java NumberCheck
                '''
            }
        }

        stage('Run - PROD') {
            when {
                expression { params.ENV == 'prod' }
            }
            steps {
                sh '''
                echo "Running in PROD environment"
                java NumberCheck
                '''
            }
        }
    }
}

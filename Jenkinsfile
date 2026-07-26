pipeline {
    agent any

    parameters {
        choice(
            name: 'ENVIRONMENT',
            choices: ['staging', 'production'],
            description: 'Target'
        )
    }

    stages {

        stage('Build') {
            steps {
                echo 'Building'
            }
        }

        stage('Tests') {
            parallel {
                stage('Unit') {
                    steps {
                        sh 'echo Unit tests'
                    }
                }

                stage('Integration') {
                    steps {
                        sh 'echo Integration tests'
                    }
                }
            }
        }

        stage('Approve') {
            when {
                expression { params.ENVIRONMENT == 'production' }
            }
            steps {
                input message: 'Deploy to production?'
            }
        }

        stage('Deploy') {
            steps {
                sh "echo Deploying to ${params.ENVIRONMENT}"
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
    }
}

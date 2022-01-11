pipeline {
    agent {
        docker {
            image 'node:16.13.1-alpine'
        }
    }
    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
        CRED = credentials('vic-github')
    }
    stages {
        /* "Build" and "Test" stages omitted */

        stage('Deploy - Staging') {
            steps {
                sh './deploy staging'
                sh './run-smoke-tests'
            }
        }

        stage('Sanity check') {
            steps {
                input "Does the staging environment look ok?"
            }
        }

        stage('Deploy - Production') {
            steps {
                sh './deploy production'
            }
        }
    }
}

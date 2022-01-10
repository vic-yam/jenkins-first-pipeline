pipeline {
    agent {
        docker {
            image 'node:16.13.1-alpine'
            label '!windows'
        }
    }
    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
        CRED = credentials('b1104a26-8af3-4dff-8fc1-c6116faada6a')
    }
    stages {
        stage('build') {
            steps {
                sh 'node --version'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}, with cread: ${CRED}"
            }
        }
        stage('Build') {
            steps {
                echo "Database engine is ${DB_ENGINE}"
                echo "DISABLE_AUTH is ${DISABLE_AUTH}"
                sh 'printenv'
            }
        }
    }
     post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}

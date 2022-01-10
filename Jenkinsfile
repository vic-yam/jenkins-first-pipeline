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
        CRED = credentials('the-id')
    }
    stages {
        stage('write-to-file') {
            steps {
                sh 'printf "Hello, Im %s" $CRED > file.txt'
            }
        }
        stage('read-from-file') {
            steps {
                sh '''
                input="file.txt"

                while IFS= read -r line
                    do
                    echo "$line"
                    done < "$input"
                '''
            }
        }
        stage('build') {
            steps {
                sh 'node --version'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''


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
            echo 'removing file.txt'
            sh '''
            FILE=file.txt
            if test -f "$FILE"; then
                echo "$FILE exists."
            else
                echo "$FILE does not exist."
            fi
            '''
            sh 'rm file.txt'
            sh '''
            FILE=file.txt
            if test -f "$FILE"; then
                echo "$FILE exists."
            else 
                echo "$FILE does not exist."   
            fi
            '''
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

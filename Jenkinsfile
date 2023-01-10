pipeline {
    agent any

    stages {

        stage('Verify Branch') {
            steps {
                echo "branch is : $GIT_BRANCH"
            }
        }

        stage('Docker build') {
            steps {
                echo "user is : $USER"
                sh 'docker images -a'
                sh '''cd azure-vote
                docker images -a
                docker build -t jenkins-pipeline .
                docker images -a
                cd ..'''
            }
        }

        stage('Start test app') {
            steps {
                sh 'chmod +x scripts/test_container.sh'
                sh './scripts/test_container.sh'
            }
            post {
                success {
                    echo "App started successfully"
                   }
                failure {
                    echo "App failed to start"
                   }
            }
        }

        stage('Run tests') {
            steps {
                sh 'python3 tests/test_sample.py'
            }
        }

        stage('Stop test app') {
            steps {
                sh 'docker-compose down'
            }
        }

    }
}

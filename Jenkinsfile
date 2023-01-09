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

    }
}

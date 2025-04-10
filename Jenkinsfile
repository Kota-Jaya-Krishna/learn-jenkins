pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 10, unit: 'SECONDS')     //pipeline will fail if it runs more than 10 sec//
        disableConcurrentBuilds()
         retry(1)
    }
    stages {
        stage('Build') {
            steps {
                sh 'echo This is build'
                //sh 'sleep 10'

            }
        }
        stage('Test') {
            steps {
                sh 'echo This is Test'
            }
        }
        stage('Deploy') {
            steps {
                sh ' echo This is Deploy'
                error 'pipeline failed'
            }
        }
    }
        post { 
        always { 
            echo "This section run always"
            deleteDir()
        }
        success {
            echo "This section will run when pipeline success"
        }
        failure {
            echo "This section will run when pipeline failure"
        }
    }
}
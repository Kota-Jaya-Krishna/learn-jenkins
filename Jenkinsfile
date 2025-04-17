pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 10, unit: 'HOURS')     //pipeline will fail if it runs more than 10 sec//
        disableConcurrentBuilds()              // we should not run two build at same time, so we need to use disableconcurrentbuilds//
        retry(1)                               // if it fails, it will run 2nd time//
    }
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
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
            when {
                expression { env.GIT_BRANCH ==~ "origin/main" }
            }
            steps {
                sh ' echo This is Deploy'
                //error 'pipeline failed'
            }
        }
        stage('Print params') {
            steps {
                echo "Hello ${params.PERSON}"                   // params is the reserved keyword //
                echo "Biography:  ${params.BIOGRAPHY}"
                echo "Toggle: ${params.TOGGLE}"
                echo "Choice: ${params.CHOICE}"
                echo "Password: ${params.PASSWORD}"
            }
        }
        // stage('Approval') {
        //     input {
        //         message "Should we continue?"
        //         ok "Yes, we should."
        //         submitter "alice,bob"
        //         parameters {
        //             string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        //         }
        //     }
        //     steps {
        //         echo "Hello, ${PERSON}, nice to meet you."
        //     }
        // }
    }
        post { 
        always { 
            echo "This section run always"
            deleteDir()             // after pipeline is triggered, we can add deletedir function,it will delete the directory where jenkins file is there
        }
        success {
            echo "This section will run when pipeline success"
        }
        failure {
            echo "This section will run when pipeline failure"
        }
    }
}
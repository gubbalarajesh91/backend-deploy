pipeline {
    agent {
        label 'Agent-1'
    }
    options {
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    parameters {
        string(name: 'appVersion', defaultValue: '1.0.0', description: 'Application version?')
    }
    environment{
        def appVersion = '' //variable declaration
    }
    stages {
        stage('print the version') {
            steps {
                script{
                    echo "Application version: ${params.appVersion}"
                }
            }
        }
        stage('Init') {
            steps {
                sh """
                    cd terraform
                    terraform init -reconfigure
                """
            }
        }
        stage('Plan') {
            steps {
                sh """
                    cd terraform
                    terraform plan -var="app_version=${params.appVersion}"
                """
            }
        }
        stage('Deploy') {
            steps {
                sh """
                    cd terraform
                    terraform apply -auto-approve -var="app_version=${params.appVersion}"
                """
            }
        }

    }




    post {
        always{
            echo 'I will always say Hello again!'
            deleteDir()
        }
        success {
            echo "run when pipeline is success"
        }
        failure {
            echo 'This will run when pipeline is failed'
        }
    }
}

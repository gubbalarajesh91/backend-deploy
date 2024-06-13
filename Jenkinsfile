pipeline {
    agent {
        label 'AGENT-1'
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
                    packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version                        //variable assigned
                    echo "Application version is $appVersion"
                }
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

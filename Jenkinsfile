@Library('Batch_31') _

pipeline {
    agent any

    environment {
        CONFIG_FILE = 'config/prod.groovy'
    }

    stages {
        stage('Deploy via Ansible') {
            steps {
                script {
                    deploy(CONFIG_FILE)
                }
            }
        }
    }

    post {
        failure {
            script {
                def conf = loadConfig(CONFIG_FILE)
                notifySlack(conf.SLACK_CHANNEL_NAME, "*Deployment FAILED* for `${conf.ENVIRONMENT}` ")
            }
        }
    }
}

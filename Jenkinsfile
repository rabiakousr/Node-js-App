pipeline {
    agent any

    environment {
        NODEJS_HOME = tool 'NodeJS 20'
        PATH = "${NODEJS_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/rabiakousr/Node-js-App'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy to Server') {
            steps {
                sshagent(['ssh-key-jenkins']) {
                    sh '''
                    scp -r * ubuntu@54.82.248.162:/root/Node-js-App/online_shop
                    ssh ubuntu@54.82.248.162 "npm run build"
                    '''
                }
            }
        }
    }
}



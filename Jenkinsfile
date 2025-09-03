pipeline {
    agent any

    stages {
        stage('Cloning Repo') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mletre/kongcicdtest.git']])
            }
        }
        stage('Test ping to the Kong Admin API') {
            steps {
               script {
                sh 'deck gateway ping'
                }
            }
        }
        stage('Validate the Deck File') {
            steps {
               script {
                sh 'deck gateway validate --workspace default deck/deck.yaml'
                }
            }
        }
        stage('Show the diff of Configuration') {
            steps {
                script {
                sh 'deck gateway diff --workspace default deck/deck.yaml'
            }
        }
        }
        stage('Apply Changes') {
            steps {
               script {
                sh 'deck gateway sync --workspace default deck/deck.yaml'
                }
            }
        }
        
    }
}
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/josiah34/Jenkins-Python-Pipeline-.git']])
            }
        }
        stage('Build') {
            steps {
               git branch: 'main', url: 'https://github.com/josiah34/Jenkins-Python-Pipeline-.git'
               sh 'python3 operations.py'
            }
        }
        stage('Test') {
            steps {
               git branch: 'main', url: 'https://github.com/josiah34/Jenkins-Python-Pipeline-.git'
               sh 'python3 -m pytest -v'
            }
            
            
        }
    }
    
    
}
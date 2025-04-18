pipeline {
    agent { label 'maven-agent' }

    stages {
        stage('Clone code') {
            steps {
                git branch: 'main', url: 'https://github.com/D-dev-2099/Deepthi-ttrend.git'
            }
        }
    }
}

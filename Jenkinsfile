pipeline {
    agent { label 'maven-agent' }

    environment {
        PATH = "/opt/apache-maven-3.9.9/bin:$PATH"
    }

    stages {
        stage('Build') {
            steps {
                echo '--------------- Build started ------------'
                sh 'mvn clean install -Dmaven.compiler.source=11 -Dmaven.compiler.target=11'
                echo '--------------- Build completed ------------'
            }
        }

        stage('Unit Test') {
            steps {
                echo '--------------- Unit Test started ------------'
                sh 'mvn surefire-report:report'
                junit '**/target/surefire-reports/*.xml'
                echo '--------------- Unit Test completed ------------'
            }
        }

        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'Valaxy-SonarScanner'
            }
            steps {
                echo '--------------- Sonar started ------------'
                withSonarQubeEnv('Valaxy-SonarQube-Server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
                echo '--------------- Sonar Completed ------------'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}

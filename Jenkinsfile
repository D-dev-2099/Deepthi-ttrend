pipeline {
    agent { label 'maven-agent' }

    environment {
        M2_HOME = "/opt/apache-maven-3.9.9"
        PATH = "${M2_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Build') {
            steps {
                echo '--------------- Build started ------------'
                sh 'mvn clean install -Dmaven.compiler.source=11 -Dmaven.compiler.target=11 -DskipTests=true'
                echo '--------------- Build completed ------------'
            }
        }

        stage('Unit Test') {
            steps {
                echo '--------------- Unit Test started ------------'
                sh 'mvn surefire-report:report'
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
}

pipeline {
    agent { label 'maven-agent' }
environment {
     PATH = "/opt/apache-maven-3.9.9/bin:$PATH"
}
    stages {
        stage('build'){
            steps {
                echo '--------------- Build started ------------'
                sh 'mvn clean deploy -Dmaven.compiler.source=11 -Dmaven.compiler.target=11 -DskipTests'
                    echo '--------------- Build completed  ------------'
            }
        }

            stage('Unit Test'){
                steps{
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
               withSonarQubeEnv('Valaxy-SonarQube-Server') { // If you have configured more than one global server connection, you can specify its name
                   sh "${scannerHome}/bin/sonar-scanner"
               }   
                    echo '---------------Sonar Competed ------------'
    }
  }
    }
}

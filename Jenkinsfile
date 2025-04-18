pipeline {
    agent { label 'maven-agent' }
environment {
     PATH = "/opt/apache-maven-3.9.9/bin:$PATH"
}
    stages {
        stage('build'){
            steps {
               sh 'mvn clean deploy -Dmaven.compiler.source=11 -Dmaven.compiler.target=11 -DskipTests'
            }
        }
    }
}

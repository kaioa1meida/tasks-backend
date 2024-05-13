pipeline {
    agent any
    stages {
        stage ("Build Backend") {
            steps {
                sh 'mvn clean package -DskipTests=true'
            }
        }
        stage ("Unit Tests") {
            steps {
                sh 'mvn test'
            }
        }
        stage ("Sonar Analysis") {
            environment {
                scannerHome = tool 'SONAR_SCANNER'
            }
            steps {
                withSonarQubeEnv('SONAR_LOCAL') {
                    sh "${scannerHome}/bin/sonar-scanner -X -Dsonar.projectKey=DeployBackend -Dsonar.host.url=http://localhost:9000 -Dsonar.login=e9935c45a3ef45decbdbe543ffe016d0e239510f -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn/**,**/src/test/**,**/model/**,**Application.java"
                }
            }
        }
    }
}



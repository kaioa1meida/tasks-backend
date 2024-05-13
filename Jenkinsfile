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
                    sh "${scannerHome}/bin/sonar-scanner -e sonar.projectKey=DeployBackend sonar.host.url=http://localhost:9000 sonar.login=e9935c45a3ef45decbdbe543ffe016d0e239510f sonar.java.binaries=target sonar.coverage.exclusions=**/.mvn/**,**/src/test/**,**/model/**,**Application.java"
                }
            }
        }
        stage () {
            steps {
                
            }
        }
    }
}



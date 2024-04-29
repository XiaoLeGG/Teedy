pipeline {
    agent any
    
    stages {
        stage('Clean') {
            steps {
                sh "mvn clean"
            }
        }

        stage('Build') {
            steps {
                sh "mvn install --DskipTests"
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test --fail-never'
            }
        }
        
        stage('Doc') {
            steps {
                sh "mvn javadoc:jar"
            }
        }
    }
    
    post {
        always {
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/surefire-reports/**', fingerprint: true

            archiveArtifacts artifacts: '**/target/*.log', fingerprint: true
        }
    }
}

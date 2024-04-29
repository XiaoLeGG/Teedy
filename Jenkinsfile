pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh "mvn clean package --fail-never"
            }
        }
        
        stage('Doc') {
            steps {
                sh "mvn javadoc:jar"
            }
        }
        
        stage('PMD') {
            steps {
                sh "mvn pmd:pmd"
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

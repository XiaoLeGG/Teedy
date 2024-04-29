pipeline {
	agent any
	stages {
		stage('Build') {
			steps {
				sh 'mvn -B -DskipTests clean package'
			}
		}
		stage('Test') {
	            steps {
	                script {
	                    junit allowEmptyResults: true, testResults: "target/surefire-reports/*.xml"
	                }
	            }
	        }
	        stage('Generate Javadoc') {
	            steps {
	                sh 'mvn javadoc:jar'
	                archiveArtifacts artifacts: 'target/site/apidocs/*', fingerprint: true
	            }
	        }
	}
	
}

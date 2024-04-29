pipeline {
    agent any
    
    stages {
        
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
            post {
                success {
                    junit '**/target/surefire-reports/*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
        
        stage('Generate Javadoc') {
            steps {
                // 生成 Javadoc
                sh 'mvn javadoc:jar'
            }
            post {
                success {
                    // 将 Javadoc 生成的 jar 文件作为 artifact
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
    
    post {
        always {
            // 清理工作目录
            cleanWs()
        }
    }
}

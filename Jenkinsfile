pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                // 使用 Maven 构建项目
                sh "mvn clean package"
            }
            post {
                artifacts {
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
        
        stage('Doc') {
            steps {
                sh "mvn javadoc:jar"
            }
            post {
                artifacts {
                    archiveArtifacts 'target/site/apidocs/**'
                }
            }
        }
        
        stage('PMD') {
            steps {
                sh "mvn pmd:pmd"
            }
            post {
                artifacts {
                    archiveArtifacts 'target/site/pmd/*.html'
                }
            }
        }
        
        stage('Test Reports') {
            steps {
                sh "mvn clean test --fail-never"
            }
            post {
                junit 'target/surefire-reports/*.xml'
            }
        }
    }
    
    post {
        always {
            // 不管构建成功或失败，都保存 Maven 日志为 artifact
            archiveArtifacts 'target/*.log'
        }
    }
}

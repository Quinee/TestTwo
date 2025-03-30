pipeline {
    agent any
    tools {
        maven 'MavenJenkins'  // Ensure this matches the name set in "Global Tool Configuration"
    }


    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Quinee/TestTwo.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    sh 'mvn clean install -DskipTests'

                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh 'mvn test'
                }
            }
        }

        stage('Publish Reports') {
            steps {
                publishHTML(target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'target/surefire-reports',
                    reportFiles: 'index.html',
                    reportName: 'TestNG Report for Test2'
                ])
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'target/surefire-reports/*.xml', fingerprint: true
            junit 'target/surefire-reports/*.xml'
        }
    }
}

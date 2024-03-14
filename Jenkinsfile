pipeline {
    agent any
    
    triggers {
        cron('H/10 * * 4')
    }
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/XiongAlex/comp367petclinic.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage('Code Coverage') {
            steps {
                sh 'mvn jacoco:prepare-agent test jacoco:report'
                publishHTML(target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'target/site/jacoco/',
                    reportFiles: 'jacoco-aggregate/jacoco.xml',
                    reportName: 'Code Coverage Report'
                ])
            }
        }
    }
}

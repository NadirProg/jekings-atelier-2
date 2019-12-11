pipeline {
	agent any
    tools {
        maven 'maven-3.6.2'
        jdk 'jdk1.8.0_211'
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn install'
            }
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml'
                }
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
			post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
		 stage('couverture') {
            steps {
                bat 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
            }
			post {
                always {
                    cobertura coberturaReportFile: '**/target/site/cobertura/coverage.xml'
                }
            }
        }
    }
}
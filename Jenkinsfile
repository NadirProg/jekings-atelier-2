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
		
		stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('My SonarQube Server') {
                    // Optionally use a Maven environment you've configured already
                        sh 'mvn clean verify sonar:sonar -Dsonar.login=844daff72e5f7a807cdf22b9fa71b5cf7e6d9a95'
                }
            }
        }
    }
}
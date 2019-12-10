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
    }
}
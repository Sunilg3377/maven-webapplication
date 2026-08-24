// dev Jenkins pipeline

pipeline {
    agent any

    tools {
        maven "maven-3.9.6"
    }

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'qa',
                    url: 'https://github.com/Sunilg3377/maven-webapplication.git'
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SQ REPORT') {
            steps {
                sh 'mvn clean package org.sonarsource.scanner.maven:sonar-maven-plugin:sonar'
            }
        }

        stage('Deploy to Nexus') {
            steps {
                sh 'mvn deploy'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                    curl -u kk:password \
                    --upload-file target/maven-web-application.war \
                    "http://100.25.246.255:8080/manager/text/deploy?path=/maven-web-application&update=true"
                '''
            }
        }

        stage('bsnl-uat') {
            steps {
                build job: 'bsnl-uat'
            }
        }
    }
}

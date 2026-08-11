pipeline {
    agent any 

    stages {

        stage('checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/devops002026-web/SampleWebApplication.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                sh 'mvn clean install' // mvn clean package 
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
                configFileProvider([configFile(fileId: 'ba1cfde0-e4e7-4537-8b4a-e05c48350215', variable: 'MAVEN_SETTINGS')]) {
                    sh 'mvn deploy -s "$MAVEN_SETTINGS"'
                }
            }
        }
    }
}
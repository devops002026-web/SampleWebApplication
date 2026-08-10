```groovy
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/devops002026-web/SampleWebApplication.git'
                    ]]
                ])
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy to JFrog') {
            steps {
                configFileProvider([
                    configFile(
                        fileId: 'ba1cfde0-e4e7-4537-8b4a-e05c48350215',
                        variable: 'MAVEN_SETTINGS'
                    )
                ]) {
                    sh '''
                        echo "Deploying artifact to JFrog Artifactory..."
                        mvn deploy -s "$MAVEN_SETTINGS" -DskipTests
                    '''
                }
            }
        }
    }

    post {
        success {
            echo '========================================'
            echo 'BUILD AND JFROG DEPLOYMENT SUCCESSFUL'
            echo '========================================'
        }

        failure {
            echo '========================================'
            echo 'PIPELINE FAILED'
            echo '========================================'
        }
    }
}
```

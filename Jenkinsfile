pipeline {
    agent any 

    stages {
        stage('checkout') {
            steps {
                checkout ({
                    $class: 'GitSCM',
                    branches : [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/devops002026-web/SampleWebApplication.git']]
                })
            }
        }

        stage ('Build') {
            steps {
                sh 'mvn clean install'  // war gets genewrated in target folder
            }
        }

        stage ('Test') {
            steps {
                sh 'mvn test' // run test cases / unit tests 
            }
        }

        stage ('Deploy') {
            steps {
                configFileProvider([
                    configFile(fileId: 'ba1cfde0-e4e7-4537-8b4a-e05c48350215',
                    variable: 'MAVEN_SETTINGS')
                ]) {
                    sh 'mvn deploy -s $MAVEN_SETTINGS'  // deploy to nexus
                }
        
            }
        }
    }
}

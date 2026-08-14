@Library('jenkins-shared-library') _


pipeline {
    agent any 

    stages {

      stage("CI/CD stages") {
        steps {
            checkout()
            build()
            test()
            deploy()
        }
      }
    }
}
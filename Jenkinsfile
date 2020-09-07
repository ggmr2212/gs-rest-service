pipeline {

    agent {
        node {
            label 'master'
        }
    }

    options {
        buildDiscarder logRotator(
                    daysToKeepStr: '16',
                    numToKeepStr: '10'
            )
    }

    stages {

        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                sh """
                echo "Cleaned Up Workspace For Project"
                """
            }
        }

        stage('Code Checkout') {
            steps {
            sh """
                         echo "Code checkout init"
                         """
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/master']],
                    userRemoteConfigs: [[url: 'https://github.com/ggmr2212/gs-rest-service.git']]
                ])
            sh """
               echo "Code checkout  end"
                        """
            }

        }

        stage(' Unit Testing') {
            steps {
                sh """
                echo "Running Unit Tests"
                mvn test
                """
            }
        }

        stage('Build Code') {

            steps {
                sh """
                echo "Building Artifact"
                mvn clean package
                """
            }
        }

    }
}
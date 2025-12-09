pipeline {
    agent any

    tools {
        jdk "java17"
        maven "Maven3.9.11"
    }

    environment {
        SONAR_HOST_URL = "https://v2code.rtwohealthcare.com"
        SONAR_TOKEN = "sqp_66f750d999ef3b09e6eb1c9364831c0de05f03fa"
    }

    stages {

        stage('Checkout') {
            steps { checkout scm }
        }

        stage('Maven Build + Tests') {
            steps {
                sh """
                    cd Sample
                    mvn -B clean verify
                """
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh """
                        cd Sample
                        mvn sonar:sonar \
                            -Dsonar.projectKey=python \
                            -Dsonar.projectName=python \
                            -Dsonar.host.url=${SONAR_HOST_URL} \
                            -Dsonar.token=${SONAR_TOKEN}
                    """
                }
            }
        }
    }
}

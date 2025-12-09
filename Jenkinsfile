pipeline {
    agent any

    tools {
        jdk "java17"
        maven "Maven3.9.11"
    }

    environment {
        SONAR_HOST_URL = "https://v2code.rtwohealthcare.com"
        SONAR_TOKEN = "sqp_ab8a0531672e6c8dee6db9a4b07b15b1ce645049"
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
                       mvn clean verify sonar:sonar \
                                 -Dsonar.projectKey=test_v5 \
                                 -Dsonar.projectName='test_v5' \
                                 -Dsonar.host.url=http://10.80.5.127:9070 \
                                 -Dsonar.token=${SONAR_TOKEN}

                    """
                }
            }
        }
    }
}

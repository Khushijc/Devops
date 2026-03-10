pipeline {
    agent any

    tools {
        maven "Maven3"
        jdk "Java21"
    }

    stages {

        stage('Initialize') {
            steps {
                echo "PATH = ${env.PATH}"
                echo "M2_HOME = ${env.M2_HOME}"
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main',
                credentialsId: 'github-token',
                url: 'https://github.com/Khushijc/Devops.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }

    }

    post {
        always {
            junit(
                allowEmptyResults: true,
                testResults: '**/target/surefire-reports/*.xml'
            )
        }

        success {
            echo 'Build completed successfully!'
        }

        failure {
            echo 'Build failed!'
        }
    }
}

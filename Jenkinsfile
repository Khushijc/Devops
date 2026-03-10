pipeline {
    agent any

    tools {
        maven "Maven3"
        jdk "JDK21"
    }

    stages {

        stage('Initialize') {
            steps {
                echo "PATH = ${M2_HOME}/bin:${PATH}"
                echo "M2_HOME = /opt/maven"
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main',
                credentialsId: 'github-token',
                url: 'https://github.com/Heramb1221/devops-p-3'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
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

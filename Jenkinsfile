pipeline {
    agent any

    tools {
        maven 'Maven3'   // Maven name you configured in Jenkins (Manage Jenkins → Global Tool Configuration)
        jdk 'Java17'     // JDK name you configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/benn-3/TomcatMavenApp.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                    cp target/*.war /var/lib/tomcat9/webapps/
                '''
            }
        }
    }

    post {
        success {
            echo 'Build and Deployment Successful ✅'
        }
        failure {
            echo 'Build Failed ❌'
        }
    }
}

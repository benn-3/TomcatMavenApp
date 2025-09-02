pipeline {
    agent any
    tools {
        maven 'Maven-3.9'  // match the Maven name in Jenkins config
        jdk 'Java17'       // if required
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/benn-3/TomcatMavenApp.git', branch: 'master'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    sh '''
                    WAR=$(ls target/*.war | head -n 1)
                    docker cp "$WAR" tomcat-container:/usr/local/tomcat/webapps/ROOT.war
                    docker restart tomcat-container
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Deployed successfully to Tomcat!'
        }
        failure {
            echo 'Build or deploy failed.'
        }
    }
}

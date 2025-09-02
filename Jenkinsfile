pipeline {
    agent any

    tools {
        maven 'Maven3'   // Must match your Jenkins Maven configuration
        jdk 'Java17'     // Must match your Jenkins JDK configuration
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/benn-3/TomcatMavenApp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker stop C1 || true'
                sh 'docker rm C1 || true'

                // Copy the built WAR from this job's workspace
                sh 'cp target/TomcatMavenApp-2.0.war /tmp/'

                // Deploy on Tomcat container
                sh 'docker run -d -p 8001:8080 -v /tmp/TomcatMavenApp-2.0.war:/usr/local/tomcat/webapps/TomcatMavenApp-2.0.war --name C1 tomcat:latest'
            }
        }
    }
}

pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'   // name configured in Jenkins Global Tool Config
        jdk 'JAVA_HOME'      // name configured in Jenkins Global Tool Config
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/benn-3/TomcatMavenApp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                sh 'cp target/*.war /var/lib/tomcat9/webapps/'
            }
        }
    }
}

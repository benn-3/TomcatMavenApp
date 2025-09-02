pipeline {
    agent any

    stages {
        stage('Deploy') {
            steps {
                // Stop and remove any existing Tomcat container (optional)
                sh 'docker stop C1 || true'
                sh 'docker rm C1 || true'

                // Copy the war file to a temporary location
                sh 'cp /var/lib/jenkins/workspace/Build-app/target/TomcatMavenApp-2.0.war /tmp/'

                // Run the Tomcat Docker container and map port 8080 in the container to port 8001 on the VM
                sh 'docker run -d -p 8001:8080 -v /tmp/TomcatMavenApp-2.0.war:/usr/local/tomcat/webapps/TomcatMavenApp-2.0.war --name C1 tomcat:latest'
            }
        }
    }
}

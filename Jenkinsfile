pipeline {
    agent any
    stages { 
        stage('Example') {
            steps {
                sh 'mvn clean compile'
            }
        }
      
      stage('Example3') {
            steps {
                sh 'mvn -e package'
            }
        }
        
        stage('Example4') {
            steps {
                sh 'scp target/mvn-hello-world.war /opt/apache-tomcat-9.0.35/webapps'
            }
        }
    }
}



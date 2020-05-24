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
    }
}



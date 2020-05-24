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
                archiveArtifacts artifacts: 'target/*'
            }
        }
        
        stage('DeployToStaging') {
            when {
                branch 'master'
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'webserver_user', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
                    sshPublisher(
                        failOnError: true,
                        continueOnError: false,
                        publishers: [
                            sshPublisherDesc(
                                configName: 'staging',
                                sshCredentials: [
                                    username: "$USERNAME",
                                    encryptedPassphrase: "$USERPASS"
                                ], 
                                transfers: [
                                    sshTransfer(
                                        sourceFiles: 'target/*',
                                        removePrefix: 'target/',
                                        remoteDirectory: '/apache/apache-tomcat-9.0.35/webapps/',
                                        
                                        
                                    )
                                ]
                            )
                        ]
                    )
                }
            }
        }
    }
}



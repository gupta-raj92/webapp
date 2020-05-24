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
                archiveArtifacts artifacts: target/myfolder.zip
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
                                        sourceFiles: 'target/mvn-hello-world.war',
                                        removePrefix: 'target/',
                                        remoteDirectory: '/tmp',
                                        
                                        
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



pipeline {   
    agent any
    stages {
        stage("test") {
            steps {
                script {
                    echo "Testing the application...."
                }
            }
        }
        
        stage("build") {
            steps {
                script {
                    echo "Building the application...."
                }
            }
        }

        stage("deploy") {
            steps {
                script {
                    sshagent(credentials: ['dev-ec2-key']) {
                        sh '''
                            ssh -o StrictHostKeyChecking=no ec2-user@3.91.192.6 "
                                docker pull kingsleychino/demo-app:1.0 &&
                                docker run -p 8080:8080 -d kingsleychino/demo-app:1.0
                            "
                        '''
                    }
                }
            }
        }               
    }
} 

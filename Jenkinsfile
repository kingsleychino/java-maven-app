pipeline {

    agent any
    tools {
        maven 'maven-3.9'
    }

    stages {

        stage("build jar") {
            steps {
                script {
                    echo "building the application..."
                    sh 'mvn package'
                }
            }
        }
        stage("test image") {
            steps {
                script {
                    echo "testing the application..."
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh 'docker build -t kingsleychino/demo-app:jma-2.0 .'
                        sh 'echo $PASS | docker login -u $USER --password-stdin'
                        sh 'docker push kingsleychino/demo-app:jma-2.0'
                    }
                }
            }
        }
        stage("deploy") {
            steps {
                echo "deploying the application..."
            }
        }
    }
}

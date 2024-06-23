pipeline {
    agent any
    tools {
        maven 'jenkins-maven'
    }
    stages {
        stage("build jar") {
            steps {
                echo "Building the Application"
                sh "mvn package"
            }
        }
        stage("build image") {
            steps {
                script {
                    echo "building docker image"
                    withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'PASS', usernameVariable: 'USER')]){
                        sh 'docker build -t a4illusionist/maven-app:2.0 .'
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push a4illusionist/maven-app:2.0'
                    }
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    echo "deploying"
                    //gv.deployApp()
                }
            }
        }
    }   
    post{
        always{
            echo "It is always"
        }
        success{
            echo "It is Success"
        }
        failure{
            echo "It is failure"
        }
    }
}
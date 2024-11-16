#!/usr/bin/env groovy
// CD - Deploy Application from Jenkins Pipeline to EC2 Instance (automatically with docker)




library identifier: 'jenkins-shared-library@master', retriever: modernSCM(
        [$class: 'GitSCMSource',
         remote: 'https://gitlab.com/Rajib-Mardi/jenkins-shared-library.git',
         credentialsId: 'gitlab-token'
        ]
)



pipeline {
    agent any
    tools {
        maven 'maven-3.9'
    }
    environment {
        IMAGE_NAME = 'rajibmardi/my-repo:java-maven-2.0'
    }
    stages {

        stage("build app") {
            steps {
                script {
                    echo 'building application jar...'
                    buildJar()
                }
            }
        }
        stage("build and push image") {
            steps {
                script {
                    echo 'building docker image...'
                    buildImage(env.IMAGE_NAME)
                    dockerLogin()
                    dockerPush (env.IMAGE_NAME)
                }
            }
        }

        stage('deploy') {
            steps {
                script {
                    echo 'deploying docker image to EC2'
                    // def dockerCmd = "docker run -p 8080:8080 -d ${IMAGE_NAME}"
                    //def dockerComposeCmd = "docker-compose -f docker-compose.yaml up --detach"

                    def shellCmd = "bash ./server-cmds.sh ${IMAGE_NAME}"
                    def ec2Instance = "ec2-user@18.142.228.154"

                    sshagent(['ec2-server-key']) {
                        sh "scp server-cmds.sh ${ec2Instance}:/home/ec2-user"
                        sh "scp docker-compose.yaml ${ec2Instance}:/home/ec2-user"
                        sh "ssh -o StrictHostKeyChecking=no ${ec2Instance} ${shellCmd}"
                    }
                }   
             }
        }
    }
}  




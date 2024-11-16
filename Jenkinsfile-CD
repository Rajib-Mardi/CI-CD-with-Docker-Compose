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
    

    stages {
        stage ('increment version') {
            steps {
                script {
                    echo 'incrementing version....'
                    sh 'mvn build-helper:parse-version versions:set \
                        -DnewVersion=\\\${parsedVersion.majorVersion}.\\\${parsedVersion.minorVersion}.\\\${parsedVersion.nextIncrementalVersion} \
                        versions:commit'
                    def matcher =readFile('pom.xml') =~ '<version>(.+)</version>'
                    def version =matcher[0][1]
                    env.IMAGE_NAME = "$version-$BUILD_NUMBER"
                }
            }
        }

        stage("build app") {
            steps {
                script {
                    echo 'building application jar...'
                    buildJar()
                }
            }
        }
stage('build image') {
            steps {
                script {
                    echo "building the docker image..."
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh "docker build -t rajibmardi/my-repo:${IMAGE_NAME} ."
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh "docker push rajibmardi/my-repo:${IMAGE_NAME}"
                    }
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
        stage('commit version update') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'gitlab-token', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh "git remote set-url origin https://${USER}:${PASS}@gitlab.com/Rajib-Mardi/java-maven-app.git"
                        sh 'git add .'
                        sh 'git commit -m "ci:jenkins-jobs"'
                        sh 'git push origin HEAD:feature/ec2-instace-docker-compose-yamlfile'
                    }

                }
            }
        }

    }
}


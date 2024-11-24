###  Demo Project:
*  Complete the CI/CD Pipeline (Docker-Compose, Dynamic versioning) 

### Technologiesused:
* AWS, Jenkins, Docker, Linux, Git, Java, Maven, Docker Hub

#### Project Description:


Create and configure an EC2 Instance on AWS
Install Docker on remote EC2 Instance and add docker to ec2-user group
* configure the security-group inbound rule in aws for jenkins IP to access the ec2-server and port no.  for java maven application.

Create ssh key credentials for EC2 server on Jenkins username as ec2-user and password as pem file of inside contents  kind as SSH username with password 
* Install the  SSH agent plugin on Jenkins to  secure SSH key authentication


* Installed Docker-Compose on EC2 Instance user use the Docker compose curl command and make it executable  the docker compose 

```
sudo curl -L https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker compose --version
```

*  Created docker-compose.yaml file
*  using docker compose we are going to start java maven application image and postgress database  container

 ### complete pipeline 

![10 - Deploy to EC2 server from Jenkins Pipeline - CI_CD Part 3 _ TechW - Brave 24-11-2024 13_58_04](https://github.com/user-attachments/assets/71fd4949-80be-474d-8adf-028a9f5102e8)

#### CI step:Increment version 
#### CI step: Build artifact for Java Maven application 
#### CI step: Build and push Docker image to Docker Hub 
#### CD step: Deploy new application version with Docker Compose
 * Configure Jenkins pipeline to deploy newly built image using Docker Compose on EC2 server.
 *  Extract multiple Linux commands that are executed on remote server into a separate ```shell script``` and execute the script from Jenkinsfile

 * This Jenkins pipeline stage (```deploy```) automates the deployment of a Docker image to an EC2 instance:
   1. Stage Name: ```deploy``` - The step is part of the deployment process.

   2. Steps:

   * Echo: Prints the message "deploying docker image to EC2" to the Jenkins console.
      * Define Variables:
      * ```shellCmd```: Defines the command to run on the EC2 instance (```bash ./server-cmds.sh ${IMAGE_NAME}```), where ```${IMAGE_NAME}``` is likely a variable representing the Docker image.
      * ```ec2Instance```: The EC2 instance's SSH details (username and IP address).
   3. SSH Agent:

   * sshagent(['ec2-server-key']): This block allows the use of a stored SSH private key (```ec2-server-key```) to authenticate when accessing the EC2 instance via SSH.
   4. Transfer Files:

        * ```scp``` commands copy the ```server-cmds.sh``` and ```docker-compose.yaml``` files from the Jenkins workspace git repository to the EC2 instance (```/home/ec2-user``` directory).
    5. SSH Execution:

        * The ```ssh``` command runs the deployment script (```server-cmds.sh```) on the EC2 instance. The ```-o StrictHostKeyChecking=no``` option avoids SSH host key verification issues.
 #### CD step: Commit the version update

#### Executed Jenkins Pipeline and deploy to AWS EC2 Instance

![feature_ec2-instace-docker-compose-yamlfile  my-multi-branch-pipeline   Jenkins  - Google Chrome 15-04-2023 17_11_52](https://user-images.githubusercontent.com/96679708/232329639-211b817e-8641-4aee-bf96-878f11594248.png)


![MINGW64__c_Users_Rajib 15-04-2023 17_32_51](https://user-images.githubusercontent.com/96679708/232329645-77e4cfeb-ce78-4e2b-a53a-5a77ed9677b2.png)

###  Demo Project:
*  Complete the CI/CD Pipeline (Docker-Compose, Dynamic versioning) 

### Technologiesused:
* AWS, Jenkins, Docker, Linux, Git, Java, Maven, Docker Hub

#### Project Description:


* Create and configure an EC2 Instance on AWS.
* Install Docker on remote EC2 Instance and add docker to ec2-user group.
* Configure the security-group inbound rule in AWS for Jenkins IP to access the EC2-server and port number for the Java Maven application.
* Create ssh key credentials for the EC2 server on Jenkins, with the username ec2-user and the password in the form of a pem file with the contents of SSH username and password.
* Install the  SSH agent plugin on Jenkins to  secure SSH key authentication.

* Installed Docker-Compose on EC2 Instance user use the Docker compose curl command and make it executable  the docker compose.
```
sudo curl -L https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker compose --version
```

*  Created docker-compose.yaml file: Using Docker Compose, start the Java Maven application image and the Progress database container.

 ### complete pipeline 

<img src="https://github.com/user-attachments/assets/71fd4949-80be-474d-8adf-028a9f5102e8" width="800">


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
 #### CD step: Commit the version update.

####  Executed Jenkins Pipeline


<img src="https://github.com/user-attachments/assets/e65b4435-72e3-4026-97e4-a7fe0884af1c" width="800">


#### Deploy to AWS EC2 Instance and java maven application and database  postgress container running


<img src="https://github.com/user-attachments/assets/7bbf52e4-0775-45b9-8dff-9e62b27a7d51" width="800">


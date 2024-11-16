###  Demo Project:
*  CD - Deploy Application from Jenkins Pipeline on EC2 Instance (automatically with docker-compose)

### Technologiesused:
*  AWS, Jenkins, Docker, Linux, Git, Java, Maven, Docker Hub

* Installed Docker-Compose on EC2 Instance
![ec2-user@ip-172-31-20-224_~ 14-04-2023 18_41_54](https://user-images.githubusercontent.com/96679708/232323227-b63c2db6-db1b-46cc-9b69-9e79a23b3c49.png)


*  Created docker-compose.yaml file

*  Configured Jenkinsfile to execute docker-compose command

   * We will use   ```script shell``` in stage deployment: 
   * Deploy our application using the AWS server by using a script.

     *IMAGE*
*  Executed Jenkins Pipeline and deploy to AWS EC2 Instance



![feature_ec2-instace-docker-compose-yamlfile  my-multi-branch-pipeline   Jenkins  - Google Chrome 14-04-2023 20_12_56](https://user-images.githubusercontent.com/96679708/232323507-0ed94f6b-60a6-4116-ada1-21663c1a47fe.png)


![ec2-user@ip-172-31-20-224_~ 14-04-2023 20_17_49](https://user-images.githubusercontent.com/96679708/232323478-78535621-0543-435a-bcf9-bb9cc8b413ea.png)

---------------------------------------

### Project:
*  Complete the CI/CD Pipeline (Docker-Compose, Dynamic versioning) 
### Technologiesused: 
* AWS, Jenkins, Docker, Linux, Git, Java, Maven, Docker Hub

#### Project Description:
#### Adjusted Jenkinsfile to include dynamic versioning   [Jenkinsfile link](https://github.com/Rajib-Mardi/AWS-Services/blob/CD-with-dockerCompose/Jenkinsfile-CD)
* Install the  SSH agent plugin on Jenkins to  secure SSH key authentication
* CI step:Increment version 
* CI step: Build artifact for Java Maven application 
* CI step: Build and push Docker image to Docker Hub 
* CD step: Deploy new application version with Docker Compose 
* CD step: Commit the version update

#### Executed Jenkins Pipeline and deploy to AWS EC2 Instance

![feature_ec2-instace-docker-compose-yamlfile  my-multi-branch-pipeline   Jenkins  - Google Chrome 15-04-2023 17_11_52](https://user-images.githubusercontent.com/96679708/232329639-211b817e-8641-4aee-bf96-878f11594248.png)


![MINGW64__c_Users_Rajib 15-04-2023 17_32_51](https://user-images.githubusercontent.com/96679708/232329645-77e4cfeb-ce78-4e2b-a53a-5a77ed9677b2.png)
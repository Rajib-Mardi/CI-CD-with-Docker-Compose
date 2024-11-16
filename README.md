# AWS-Services

## Demo Project:
*  CD - Deploy Application from Jenkins Pipeline to EC2 Instance (automatically with docker)

## Technologiesused:
*  AWS, Jenkins, Docker, Linux, Git, react,nodejs ,Docker Hub

### Demo 1 executed - Deploy WebApp Container via Jenkins Pipeline on EC2 Instance:

* Installed SSH agent plugin on Jenkins

![Available plugins - Plugin Manager  Jenkins  - Google Chrome 14-04-2023 11_12_28](https://user-images.githubusercontent.com/96679708/232266677-8fef5acc-0b91-4ea7-81d0-d511071934d5.png)


* Created ssh credentials type for EC2 on Jenkins
![my-multi-branch-pipeline » Folder » Global credentials (unrestricted)  Jenkins  - Google Chrome 16-04-2023 10_00_22](https://user-images.githubusercontent.com/96679708/232266723-1395008c-5ed7-47f8-9683-1085759f9713.png)


*  Configured Jenkinsfile to use the sshAgent and execute docker run command 
on EC2

  
  ![my-multi-branch-pipeline » Folder » Global credentials (unrestricted)  Jenkins  - Google Chrome 16-04-2023 10_03_58](https://user-images.githubusercontent.com/96679708/232274719-f7d83a74-da83-4771-8a3b-825a0383b6f2.png)

  
*  Docker Login to DockerHub or your other private Docker Repository (if you haven’t already)
*  Security Group configured: Added Jenkins IP Address and opened port to access Web App from Browser 

![EC2 Management Console - Google Chrome 14-04-2023 12_24_40](https://user-images.githubusercontent.com/96679708/232274808-a3287246-c6b3-4b30-88b6-4513152076bd.png)

 
* Deploy Webapp on EC2 Instance by executed Multi-Branch Pipeline

![EC2 Management Console - Google Chrome 14-04-2023 12_27_48](https://user-images.githubusercontent.com/96679708/232274850-a78db942-89b8-486a-a505-4cbb53db6638.png)



* as we can see the container is running 

![ec2-user@ip-172-31-20-224_~ 14-04-2023 13_18_14](https://user-images.githubusercontent.com/96679708/232275690-4a390cd7-0d85-4888-8711-f3482a415744.png)

*  Access Application on port 3080 in the browser


![EC2 Management Console - Google Chrome 14-04-2023 12_30_05](https://user-images.githubusercontent.com/96679708/232275037-53398831-eca1-409e-862d-4b06376ec119.png)

## Technologiesused:
*  AWS, Jenkins, Docker, Linux, Git, Java, Maven, Docker Hub

### Demo 2 executed - Deploy Java Maven App via Jenkins Pipeline on EC2 Instance:
 * Configured Jenkinsfile to build and deploy on EC2 Instance(see in feature/jenkinsfile-sshagent1 for jenkinsfile)

   * Extend the previous CI pipeline with deploy step to ssh into the remote EC2 instance and deploy newly built image from Jenkins server
 * Executed Multi-Branch Pipeline on Jenkins

![feature_jenkinsfile-sshagent1  my-multi-branch-pipeline   Jenkins  - Google Chrome 14-04-2023 13_16_48](https://user-images.githubusercontent.com/96679708/232276547-f007266b-677f-4ec5-a665-00375c8abfd4.png)


* as we can see the container is running 

![ec2-user@ip-172-31-20-224_~ 14-04-2023 13_18_14](https://user-images.githubusercontent.com/96679708/232275690-4a390cd7-0d85-4888-8711-f3482a415744.png)

*  Access Application on port 8080 in the browser

-------------------------------------------------------------------------------------



##  Demo Project:
*  CD - Deploy Application from Jenkins Pipeline on EC2 Instance (automatically with docker-compose)

## Technologiesused:
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


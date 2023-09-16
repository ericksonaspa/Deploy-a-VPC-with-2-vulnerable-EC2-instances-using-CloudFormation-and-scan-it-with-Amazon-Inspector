# Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector

CloudFormation allows you to model your infrastructure in a text file either JSON or YAML to describe what AWS resources you want to create and configure. CloudFormation automates the provisioning and updating of your infrastructure in a safe and controlled manner. There are no manual steps or controls that can lead to errors. CloudFormation is available at no additional charge. You pay only for the AWS resources needed to run your applications.

In this project, you will be using two (2) .yaml templates which will be used in creating our infrastructure in AWS. This project will be deployed together with two (2) vulnerable EC2 instances that have exposed ports. Then, we will be using the AWS Inspector to scan our EC2 instances. 

As we all know, Amazon Inspector is a vulnerability management service that continuously scans your AWS workloads for software vulnerabilities and unintended network exposure. It automatically discovers and scans running Amazon EC2 instances, container images in Amazon Elastic Container Registry (Amazon ECR), and AWS Lambda functions for known software vulnerabilities and unintended network exposure.

The architecture diagram of our project is provided below: 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/d87eca0e-e860-4717-83eb-d883ab0d597d)

The following items are contained in this project.

- Create your VPC (Internet Gateway, Public Subnets, Route tables, and Security Groups) using **Project-VPC.yaml** template
- Create your EC2 Instances using **Project-EC2.yaml** template

## DOWNLOAD THE TEMPLATES FROM THIS REPOSITORY

1. Download the two (2) Cloudformation templates from the links below:

- [VPC Cloudformation Template](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/blob/main/Project-VPC.yaml)
- [EC2 Cloudformation Template](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/blob/main/Project-EC2.yaml)

2. Once done, go to your AWS Management Console and look for the CloudFormation. Open it in a new tab.

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/cc03c3b7-107f-480b-a018-39186d924db8)

3. On the Cloudformation, look for the **Create Stack** button and click on it. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/6fcaa7f8-d53c-4152-8fb5-3ed09f374776)

4. For the **Prerequisite - Prepare Template**, choose **Template is ready**. Then on the **Specify template**, choose **Upload a template file**. Click the **Choose file** button, then locate the VPC template you downloaded earlier. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/ed916f5b-8a7a-439c-974e-58d43c38e831)

Once done, click on **Next**. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/e37f0e50-d26b-4aaa-807c-cf9f20b5d255)

5. Put a name on the **Stack name** field. Scroll down and hit **Next**. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/b9006198-ff82-44ba-84c6-ddd2f48f71f9)

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/d94ccfc9-8f73-4e49-8513-2b1cad37bf99)

6. Leave the default values on the **Step 3 - Configure stack options**. Scroll down and hit **Next**. On the next page, review the details of your stack, scroll down, and then click **Submit**. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/1068c97f-9562-4d01-9496-ecb29291e875)

7. Wait until the status of your current stack is **CREATE_COMPLETE**. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/c415213d-6517-4384-8c20-10bb1eced4f7)

8. To upload our second .yaml template, look at the right side of the screen and then go to **Create stack > With new resources (standard)**. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/4b8be970-0a54-46de-8add-99ec406b577f)

9. Follow the steps above from 4 to 7. 

10. Once both templates are uploaded and created successfully, we'll verify if the **Resources** in our templates that are expected to be created are both in the **VPC** and **EC2 dashboard**. From your CloudFormation screen, search for the **vpc** and then open it in a new tab. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/81a65a8e-25c8-492a-a785-f59d9ebaccf2)

11. On the VPC dashboard, click under the **Filter by VPC:** and then select the checkbox for the **Project VPC**. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/a10b22c5-7cec-44c4-afc0-f2af1e7f51f8)

12. Click on the **Your VPCs** under the **Virtual private cloud**, and then select the checkbox for our VPC. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/6ef3025e-a20b-49cd-866d-a0213899680d)

As what you can see, the **IPv4 CIDR** is the value we have indicated in the Parameters of our VPC template. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/bb886066-cd3f-4aaa-83f6-efc1c6525024)

13. On the Subnets, you can see that these are the CIDR we have indicated in the Parameters of our VPC template. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/8f20fbb2-9fd3-484f-8c79-ea0381b4f7fd)

See below the comparison with our code: 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/7af66448-a7f3-48c5-923f-1cdc4f82ab4b)

14. On the Route tables, you can see that in our route table, we have two (2) subnets associated. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/37766457-499d-4291-9968-c1d77fe8fe7b)

The same on the **Routes** tab, which shows that any IPv4 address with destination **0.0.0.0/0**, the target is our **Internet Gateway**.  

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/dbfa696f-5ef5-4e72-b359-c393c0a43591)

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/e7746d05-5688-4bd7-bad6-f2d2f04d74f3)

15. For the **Internet Gateway**, the Keys and Values are correct same as our .yaml code. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/7a09b6e9-b4e4-48ce-9194-7d5e4bb06b43)

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/4bfd183d-9740-4aad-9078-7739866fba4b)

16. Lastly, our Security Groups have exposed ports for inbound traffic. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/65a77bd5-3dbc-442c-9579-422da8d389a5)

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/78f92d39-e6bf-45eb-9f05-0ba3e212614c)

See the comparison with our code below: 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/b898488e-6941-4ce6-998b-867a51c7fbfa)

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/db3a1b7d-a325-4960-80cd-02da58f38900)

Now that we have verified that all of our resources are deployed, we'll go ahead and perform a scan with our AWS Inspector. 

## Perform a scan with Amazon Inspector

1. On your VPC Dashboard, search for the **Amazon Inspector** and then open it in a new tab. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/749e049e-be09-4152-9d11-d3cd34c184be)

2. Scroll down and click the **Switch to Inspector Classic**. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/614d487a-f49b-49ef-af7b-3501327b5e77)

3. Another browser tab will open, click on the **Get Started**. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/f92676b8-47b4-4610-9fb9-c193738e3a90)

4. On the Welcome screen, look at the bottom-right and then click the **Advanced Setup**. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/686f1cf8-bdf9-49bc-8872-760fe233c975)

5. We will now proceed with defining our assessment target. You may change the **Name**, it is up to you. Ensure that the checkboxes for both **All instances** and **Install Agents** are selected. Hit **Next**. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/86a326f9-24d4-4b67-807a-5910bd4b5bb7)

6. On the **Define an assessment template**, put a name on the **Name** field. It's up to you to leave the default. Choose all the **Rules packages**. Set the **Duration** to **15 Minutes** only. Uncheck the **Assessment Schedule**, and then hit **Next**.  

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/82561231-2454-4b15-8e49-7af620e17161)

7. Review the details and ensure that all are correct. Scroll down and hit **Create**.

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/8e807f75-a8a5-4f80-abf8-a6c422067b80)

8. You'll see that the assessment template we created is being prepared to start. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/0f654472-6fed-4567-b91c-1ff0d4bc7ca5)

9. Wait until the status changes to **Analysis Complete**. Tick the checkbox, you will observe that it has 8 findings with the start and end of the assessment duration. Click on the numbers found on **Findings**. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/e5833652-03f1-435c-9aad-cb8899daf258)

10. As what you can see, these are the potential security issues found after running the assessment with our Amazon Inspector. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/1f89b99c-5481-4d38-a8a7-349c512af6b9)

11. To view the full details of each finding, click the arrow to expand.

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/285f9e13-cf4c-4f8a-ae79-89884e5588e3)

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/71f84cbd-9c0c-4e9f-b9c8-f45ea2a4ccae)

12. In this example, the recommendation is to modify the security to remove the access from the internet on port 21 (FTP). 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/91e7fe28-2a2a-46b6-8de9-1f79793d4e6d)

13. It will take you to another tab. From there, you may now proceed with editing the inbound rules. 

![image](https://github.com/ericksonaspa/Deploy-a-VPC-with-2-vulnerable-EC2-instances-using-CloudFormation-and-scan-it-with-Amazon-Inspector/assets/77118362/ace52045-8cd4-494e-8822-7c6fca48d240)

Congratulations! You have finished this walkthrough and learned how to deploy and read CloudFormation templates. Also, you have learned how to set up your assessment for your EC2 instances and run a scan to identify potential security issues and remediate them. 

For more information about the two (2) services we have used, kindly refer to the following links: 

- [AWS CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)
- [Amazon Inspector](https://docs.aws.amazon.com/inspector/latest/user/what-is-inspector.html)

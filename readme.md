# This is a sample app to test AWS CodeDeploy.
 
 
 You can use this to test the deployments made by CodeDeploy to set up the environment. And when you are comfortable with deploying this sample app, it will be easy for you to Deploy your production app.

 Let me know in the issues if you want a specific part to test and want me to update the code accordingly.


 Thanks and Cheers.

# Steps to Deploy

-----------------------------------
STEP 1:  Create an IAM Role. 
-----------------------------------
- Go to the IAM console and select 'create role'.
- The EC2 service is going to use this role so select EC2 from the list of servies.
- Attach the following roles:  AmazonS3FullAccess, AWSCodeDeployFullAccess, AWSCodeDeployRole

-----------------------------------
STEP 2:  Launch the instance, Attach IAM role for permissions and install CodeDeploy Agent
-----------------------------------

- Launch an EC2 instance.
- Attach the previously created IAM role to this instance.
- Open port 443 and 80 in Security Group.
- Add the following user-data

----
user-data
----

     #!/bin/bash
     yum install update -y
     yum install ruby -y
     yum install jq -y

     cd /home/ec2-user
     wget https://aws-codedeploy-us-east-1.s3.amazonaws.com/latest/install
     chmod +x ./install
     ./install auto
     service codedeploy-agent start

-----

Please find more information on setting up your EC2 instance here:
     https://docs.aws.amazon.com/codedeploy/latest/userguide/instances-ec2-create.html

The installation steps for CodeDeploy Agent are mentioned in the given doc :
    https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-install-linux.html


-----------------------------------
STEP 3: Create Application and Deployment Group in the CodeDeploy console.
-----------------------------------
 - You can create the application and deployment group using the CLI following this doc:
    https://docs.aws.amazon.com/codedeploy/latest/userguide/tutorials-windows-upload-application.html

 - The steps 2, 3 and 4 in the above documentation instructs on how to create the deployment.

 - Using the console, create an Application and a deployment group and add the above prepared instance to that group.

 - Attach a service role which permits CodeDeploy to use the following roles:  AutoScalingFullAccess(If using Blue/green deployments), AmazonS3FullAccess,  AWSCodeDeployRole. Please feel free to change these policies as per needs.

-----------------------------------
STEP 5: Create Deployment
-----------------------------------

- Create the deployment in the above created deployment group but instead of S3, please use the Github Repository to test the deployment out.

[Please use the github repository only as a reference to expedite your work on your own discretion and do not use it in production unless tested properly]

-----------------------------------------------------------

## Setup

In this section we are going to use a CloudFormation template to perform the following actions:  

* Create a destination bucket in your account where the dataset will be placed. We will refer to this bucket as `<workshop-bucket>` through the rest of the instructions.
* Copy the dataset over from the workshop source location to the destination  `<workshop-bucket>`. 
* Create the IAM role that grants AWS Glue permissions to work with the dataset


1. Click the **Launch Stack** link below for the region of your choice.

	Region| Code | Launch
	------|------|-------
	US East 1 (North Virginia) | <span style="font-family:'Courier';">us-east-1</span> | [![Launch stack in us-east-1](images/cfn-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=saws&templateURL=https://s3.amazonaws.com/gmenende-shared-files/analytics-workshop/cfn/setup.yaml)

1. Click **Next** on the *Specify Template* page.

1. On the *Specify stack details* page, leave all the defaults and click **Next**.

1. On the *Configure stack options* page, also leave all the defaults and click **Next**.

1. On the Review page, check the boxes to acknowledge that CloudFormation will create IAM resources and a new Transform and click **Create Stack**.

	![Acknowledge IAM Screenshot](images/0a-cfn-create-change-set.png)
    
2. Wait for the `saws` stack to reach a status of `CREATE_COMPLETE` (you might need to click the refresh button to see the stack being created). 

3. Click on the **Outputs** tab. Review the artifacts created: 
	* An S3 bucket that holds the dataset: `<workshop-bucket>`
	* An IAM role for AWS Glue: `DefaultAWSGlueServiceRole`

	![CloudFormation Outputs Screenshot](images/0c-cfn-outputs.png)


### Congratulations! You completed the setup

[Proceed to next section](02-data-catalog.md)

[Back to home page](README.md)

[Back to top](#setup)








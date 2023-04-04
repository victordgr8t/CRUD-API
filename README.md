![aws-serverless](https://user-images.githubusercontent.com/63635704/229672687-d1e11026-0d83-4466-bf5f-26d2bf231e20.jpg)



# Build a CRUD RESTful Microservice with AWS Lambda, API Gateway and DynamoDB using AWS SAM and VSCode

Serverless architectures have become increasingly popular in recent years, as they offer several benefits over traditional server-based architectures. One of the key advantages of serverless architectures is that they enable you to focus on writing code instead of managing servers. In this tutorial, I'll show you how to build a serverless CRUD RESTful microservice using AWS Lambda, API Gateway, and DynamoDB using the AWS Serverless Application Model (SAM) and VSCode.

Serverless Architecture

Just in case you are a beginner in cloud, I will explain the term 'SERVERLESS' so you can have a brief understanding of what it means.

Serverless architecture is a cloud computing model where a third-party provider manages the infrastructure and handles server operations automatically. This means that developers do not have to manage servers or infrastructure themselves, and they can focus on writing code and building applications.

In a serverless architecture, the cloud provider automatically provisions and manages the server resources needed to run the code, and bills the developer based on the actual usage of resources, rather than a fixed amount. This can lead to cost savings, as the developer only pays for what is used.

Serverless architectures typically involve writing small, single-purpose functions that are triggered by events, such as a user uploading a file or a message being sent to a queue. These functions are run on demand and scaled automatically based on the number of requests received.

Serverless from the name doesn't mean that servers are not involved, it means the cloud developer shouldn't worry about provisioning, deploying and maintaining servers. Just focus on the codes that will be used for deployment. The best part is that, in a serverless architecture, you are billed based on the actual usage of resources rather than a fixed amount. This means that you are only charged for the number of computing resources and time that your code uses.

For example, if you create a function that runs for 100 milliseconds and is triggered 100 times in a month, you will only be billed for the total time that your function runs, which would be 10 seconds (100 x 0.1 seconds). The exact pricing model varies by cloud provider, but generally, you will be charged based on the number of requests, the duration of each request, and the amount of memory used.

I will be utilizing Infrastructure as Code tools, such as Serverless Architecture and AWS Serverless Application Model (SAM), throughout this article. By doing so, deploying the entire architecture on AWS will only require a few simple commands. Before we dive in, let's take a moment to familiarize ourselves with Infrastructure as Code (IaC), AWS SAM (Serverless Application Model) and CRUD REST API.

Infrastructure as code (IaC)

Infrastructure as Code (IaC) is the practice of managing and provisioning technology infrastructure using machine-readable definition files, rather than manual configuration. This approach enables teams to automate the process of deploying and managing infrastructure, resulting in faster and more consistent deployments.

At a low level, IaC involves writing code to define the resources and configurations needed for a particular infrastructure, such as servers, databases, load balancers, and other components. The code is typically written using a domain-specific language (DSL) that is specific to the infrastructure provider, such as AWS CloudFormation, Terraform, or Azure Resource Manager.

AWS SAM (Serverless Application Model)

AWS Serverless Application Model (SAM) is an open-source framework for building serverless applications using AWS services. SAM extends AWS CloudFormation to provide a simplified way of defining the Amazon API Gateway APIs, AWS Lambda functions, and Amazon DynamoDB tables needed by your serverless application. SAM also provides tools for locally testing and debugging serverless applications, as well as deploying them to AWS. With SAM, developers can quickly and easily build and deploy serverless applications on AWS.

CRUD REST API

A CRUD REST API is a RESTful API that allows for Create, Read, Update, and Delete operations on resources through HTTP methods. REST stands for Representational State Transfer, and is a set of architectural principles for designing web applications.

In a CRUD REST API, each resource is identified by a unique URL, and the HTTP methods are used to perform operations on the resource. The HTTP methods used are:

POST: used to create a new resource

GET: used to retrieve an existing resource or a collection of resources

PUT: used to update an existing resource

DELETE: used to delete an existing resource

Now we have had some brief explanations of the technologies we will use. It's about time we use Serverless Framework and AWS SAM (Serverless Application Model) to deploy our application on AWS using VScode as our cloud development environment (CDE).

AWS SAM will be creating a Lambda function, DynamoDB table and API Gateway (REST API) using our CDE VSCode. We will be issuing some commands on our terminal to deploy mentioned resources.

Prerequisites

Before we get started, you'll need the following:

An AWS account

VSCode and the AWS Toolkit extension installed

The AWS SAM CLI installed

Basic knowledge of Node.js and the AWS SDK

Confirm installation of AWS CLI and AWS SAM using commands:

$ aws --version
-> aws-cli/1.27.32 Python/3.10.10 Darwin/21.6.0 botocore/1.29.32
$ sam --version
->SAM CLI, version 1.66.0

Creating an AWS SAM project

First, we'll create a new AWS SAM project using the sam init command. Open a terminal window on VSCode and navigate to a directory where you want to create the project. You will get a prompt like below:

Choose the options from the prompt like below:

You should get these files automatically added by AWS SAM. You can inspect the files to have a better understanding of what SAM is building.

Next Step: input sam build in your terminal which will build and package serverless applications before they are deployed to AWS.

Next command: sam deploy --guided

"Sam deploy --guided" is a command used in the AWS Serverless Application Model (SAM) that initiates a guided deployment process for your serverless application. When you run this command, SAM will prompt you to answer a series of questions about your deployment, such as the AWS Region to deploy to, the name of the stack to create, and any input parameters required by the stack.

This command sam deploy --guided provides a step-by-step guided experience that helps to ensure that your deployment is configured correctly and follows best practices. It also helps to identify and resolve any potential issues or errors before the deployment process begins.

After SAM has deployed all the resources required for the CRUD REST API, you will see the invoke URL below. Copy and put in a text file as we will be testing it later.

Confirmation of SAM deployment

Log into the AWS Management Console, and search for DynamoDB, API Gateway, CloudFormation and Lambda one after the other to investigate if it was deployed successfully.

The YAML template file generated by the sam init command in AWS Serverless Application Model (SAM) is used to deploy your serverless application using AWS CloudFormation. if you inspect CloudFormation you will see the template.yaml SAM generated was used to deploy our resources in AWS.

TESTING THE CRUD API

There are several API testers, but for this tutorial, Talend API tester will be used.

Talend API Tester is a tool that is designed to test the API's of web services and RESTful services. With this tool, developers and testers can simulate API calls, generate test cases, and perform functional and performance testing of APIs.

Talend API tester is a chrome extension that can be added to your chrome browser. You can get it from the chrome store.

Open the Talend extension and input the invoke URL you saved in a text file earlier, select GET method, then click send. You should get an empty string ' [ ] ' the simple reason being that DynamoDB is empty.

To populate DyanmoDB we will use the POST method, then input some code in BODY. You should get a 200 response confirmation. After you click send, you can change the values in the body to add more items to DynamoDB.

If POST Method worked perfectly, change to GET Method to confirm if we successfully added items to DynamoDB. You should get a 200 response.

Goto DynamoDB to confirm

Now we can confirm that we have successfully built a CRUD RESTful Microservice API using AWS SAM. This method saves a lot of time, code debugging and troubleshooting. To understand this fully, you have to configure or build it manually which I will do in my next blog post.

ADDING API KEYS

To add API Keys that will restrict and grant access to selected users.

To add API keys to your CRUD API on AWS API Gateway, you can follow these steps:

Create an API key: In the AWS Management Console, navigate to the API Gateway service and select "API Keys" from the left-hand menu. Click on "Create API Key" and follow the prompts to create a new API key.

Enable API key usage: In the same "API Keys" menu, select "Usage Plans" and create a new usage plan if you haven't already. Select the usage plan and click on "Add API Key" to add the API key you just created to the plan.

Deploy the API: To deploy your API, first click on 'Resources' in the left-hand menu. Then, click on 'GET' and select 'Method Request'. Set 'API Key Required' to 'True'. To deploy the API, click on 'Actions' and select 'Deploy API'. Make sure to deploy the API whenever you make any changes for the changes to take effect.

Test the API: Test the URL on your browser to confirm that it requires API Key for access. If you Test on Talend API tester you will get a 403 error response.

To add our API keys and enable access, click on 'API Keys' in the left-hand menu of the API created by SAM. Then, click on the previously created key name and click on 'Show' next to 'API Key'. Copy the key into a text file and save it for later.

Next, go to Talend API Tester, select the 'GET' method and input the URL. Scroll down one step to the headers section and input the default header for API Keys, X-Api-Key , and paste in the API key as the value. Finally, click 'Send'. You should now receive a 200 response.

MONITORING API CALLS

Monitoring API calls using CloudWatch involves configuring CloudWatch to capture and log relevant API call data, such as API Gateway requests, Lambda function invocations, and other metrics.

To view CloudWatch logs, open the Lambda function created by SAM, click "Monitor", then "Logs". Select the logstream of the recent invocations, which will take you to CloudWatch to view logs.

From here, you can use CloudWatch to analyze and visualize your API call data. For example, you can create CloudWatch dashboards to track key metrics, set up CloudWatch alarms to alert you when specific metrics cross a threshold, and use CloudWatch Insights to perform ad-hoc queries and analysis on your log data.

In addition to CloudWatch, AWS provides other tools for monitoring and analyzing your API calls, such as AWS X-Ray and Amazon CloudTrail. AWS X-Ray is a service that lets you trace requests made to your API and identify performance bottlenecks or issues. Amazon CloudTrail is a service that records AWS API calls and events and provides visibility into user and resource activity.

By using CloudWatch, AWS X-Ray, and Amazon CloudTrail together, you can gain comprehensive visibility into your API calls and ensure that your application is running optimally and securely.

CLEANUP

You need to clean up your AWS account to avoid incurring unnecessary fees.

In VSCode type, sam destroy

'sam destroy' is a command in the AWS SAM CLI that removes the AWS CloudFormation stack associated with your SAM application. This command deletes all resources that were created when the stack was created, including the API Gateway, Lambda functions, DynamoDB tables, and any other resources defined in the CloudFormation template.

SUMMARY

In conclusion, deploying a CRUD RESTful API using AWS SAM is a straightforward process that allows you to quickly and easily build and deploy your API. With AWS SAM, you can easily manage your serverless applications and scale your infrastructure as your needs grow.

The process involves designing and creating the API using an API design tool and AWS SAM, developing and testing the API locally with the AWS SAM CLI, packaging and deploying the application using AWS CloudFormation, testing the deployed API using a tool like Postman or Talend API Tester, and monitoring and troubleshooting the API using AWS CloudWatch.

By following the steps outlined in this post, you can get your API up and running in no time. So, whether you're building a new API or migrating an existing one, AWS SAM is a powerful tool that can help you get the job done quickly and efficiently.

Hope you enjoyed the tutorial. Good luck and happy coding...



https://vicmode.hashnode.dev/build-a-crud-restful-microservice-with-aws-lambda-api-gateway-and-dynamodb-using-aws-sam-and-vscode

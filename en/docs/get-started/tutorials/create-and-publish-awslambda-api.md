# Create and Publish an AWS Lambda API

When using AWS Lambda, you can execute your code without having to manage or provision servers. For more information on AWS Lambda, see [What is AWS Lambda?](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html).

Follow the steps below to create and publish an AWS Lambda API:

## Step 1 - Design a REST API

1. Sign in to WSO2 API Cloud. This opens the API Publisher portal..

2. Click **CREATE API** and then click **Design a New REST API**.

     ![](../../assets/img/tutorials/create-api-design-rest-api.png)

3. Enter the API details and click **CREATE**.  

     ![](../../assets/img/tutorials/create-test-api.png)

    !!!note
         **You do not need to enter the Endpoint during the initial process of creating the API.**
         For more information on the possible API details that you can add, see [Design New REST API](../../../learn/design-apis/design-new-rest-api)

Now, you have designed a new REST API successfully. 

## Step 2 - Add an AWS Lambda endpoint

1. Click **Endpoints** to navigate to Endpoints page.
2. Navigate to the **AWS Lambda** endpoint type and click **ADD**.

     ![](../../assets/img/tutorials/select-awslambda-endpoint.png)

3. Select the preferred **Access Method**

    AWS SDK needs AWS credentials including the AWS region to invoke AWS Lambda functions. The access method defines as to how you provide those AWS credentials. You can provide AWS credentials and the AWS region manually by selecting the **Using stored AWS credentials** method. But if WSO2 API Manager is running on an Amazon EC2 instance, you can select the **Using IAM role-supplied temporary AWS credentials** method.

    !!!note
         When using the **IAM role-supplied temporary AWS credentials** method, you need to attach an IAM role so that it can grant permission to applications running on the Amazon EC2 instance.
         For more information on attaching an IAM role to EC2, see [Using an IAM Role to Grant Permissions to Applications Running on Amazon EC2 Instances](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-ec2.html)

4. Click **Save**.

     ![](../../assets/img/tutorials/save-awslambda.png)

    !!!note
         You will get an error message if you have not set the Access Method properly.

## Step 3 - Map function-ARNs to resources

!!!note
    For more information on ARNs, see [Amazon Resource Names (ARNs)](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html).

1. Click **Resources** to navigate to the Resources page.
2. Configure the resources.

     By default, the API will have five resources with `/*` as the URL pattern.

    1. Click delete to remove all existing resources.

         ![](../../assets/img/tutorials/delete-all-existing-resources.png)

    2. Add a new resource.
          1. Select **POST** as HTTP Verb.
          2. Enter a meaningful name for URI Pattern.
          3. Click **(+)** to add a new resource.

            ![](../../assets/img/tutorials/add-new-resource.png)

3. Under AWS Lambda Settings, select or type Amazon Resource Name (ARN) for the resource.

    You can select already created AWS Lambda functions that are listed in the autocomplete box.

      ![](../../assets/img/tutorials/add-amazon-resource-name.png)

4. Optionally, change the AWS SDK Client Execution Timeout by changing the **Set Timeout** option.
     The default AWS SDK Client Execution Timeout is 50 seconds.

     - Min Timeout - 1 second
     - Max Timeout - 15 minutes

      ![](../../assets/img/tutorials/resource-set-amazon-resource-timeout.png)

5. Click **SAVE**.

     ![](../../assets/img/tutorials/save-resource.png)

## Step 4 - Publish the AWS Lambda API

1. Click **Lifecycle** to navigate to the API lifecycle.
2. Click **PUBLISH** to publish the API to the API Developer Portal.

     ![](../../assets/img/tutorials/test-api-lifecycle.png)

You have successfully published the AWS Lambda API.
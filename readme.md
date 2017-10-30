## SSSumo
S3 - Lambda - Sumologic

#### About
This repo contains AWS Lambda code that watches an S3 bucket for new incoming objects. Then runs the code to push those new object into SumoLogic.

##### AWS Lambda setup
The Lambda function used for this example needs to have a trigger setup to look for newly created objects to a particular s3 bucket and prefix. Once new objects are dropped in a trigger will fire an event into the Lambda function and the code will run.
Your Lambda function will need to have the correct privligest to the s3 bucket. In this case read permissions is suffice.

##### SumoLogic
To allow the objects to be pushed into Sumologic a http collector needs to be set up on the platform. Once this collector is set up you will get a secret URL which you can use to post your objects to. See Sumologic documentation [here](https://help.sumologic.com/Send_Data/Sources/02Sources_for_Hosted_Collectors/HTTP_Source/Upload_Data_to_an_HTTP_Source)

##### AWS deployment
This code depends on the requests package to post data to Sumologic. This package does not belong in the standard python library nor in AWS library (like boto3 does). To capture this dependancy the requests source code is placed in the project folder and zipped up together with the source code. When deployed on AWS the library will sit in your python path, and can be used as normal. NOTE: Any library dependancies must be placed at the top level of your project home. AWS documentation [here](http://docs.aws.amazon.com/lambda/latest/dg/lambda-python-how-to-create-deployment-package.html)

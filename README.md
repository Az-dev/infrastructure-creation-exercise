# Instructions

## Step 1. Set up a CircleCI project

## Step 2. Set up Environment variables in CricleCI project

***
To use the AWS CLI in your jobs you'll need to the following environment variables to the in Circle CI > Project Settings > environment variables. The value of these variables can be fetched from the AWS IAM user.

If not already, create an AWS IAM user with programmatic access, and it will generate these credentials.
***

```
AWS_ACCESS_KEY_ID
AWS_DEFAULT_REGION
AWS_SECRET_ACCESS_KEY
```
>
Note - While saving the environment variables in the Circle CI project settings, use capital case as discussed in this thread and also mentioned here (see the DEFAULT column for the correct names).
Another useful reference: Setting an environment variable in a project. Do read about the various types of environment variables and their relative priorities.

## Step 3. Create the CloudFormation template

***
Create a simple template - template.yml that will create an EC2 instance and the associated security group. This should be pushed into your git repo.
***

## Step 4. Create"Add pipline logic to" the CircleCI Config file

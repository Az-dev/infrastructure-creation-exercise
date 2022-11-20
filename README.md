# Instructions
### Step 1. Set up a CircleCI project
### Step 2. Set up Environment variables in CricleCI project
*To use the AWS CLI in your jobs you'll need to the following environment variables to the in Circle CI > Project Settings > environment variables. The value of these variables can be fetched from the AWS IAM user.
If not already, create an AWS IAM user with programmatic access, and it will generate these credentials.*
```
AWS_ACCESS_KEY_ID
AWS_DEFAULT_REGION
AWS_SECRET_ACCESS_KEY
```
>*Note - While saving the environment variables in the Circle CI project settings, use capital case as discussed in this thread and also mentioned here (see the DEFAULT column for the correct names).
Another useful reference: Setting an environment variable in a project. Do read about the various types of environment variables and their relative priorities.*
### Step 3. Create the CloudFormation template
*Create a simple template - template.yml that will create an EC2 instance and the associated security group. This should be pushed into your git repo.*
### Step 4. Add a new Job in the CircleCI Config file ```create_infrastructure```
* Create a job in your Circle CI config file named ```create_infrastructure```
* ```create_infrastructure``` should be:
    - using ```amazon/aws-cli``` docker image that has AWS CLI installed already.
    - executing the CloudFormation template to create the infrastructure.
* Add the ```create_infrastructure``` job to the workflows section.
### Step 5. Save the SSH key pair to CircleCI
*You need to give your CircleCI job access to your SSH keys saved in your Circle CI account.*
* Open the key pair xxxx.pem file in any text editor on your local machine and copy the content.
* Go to CircleCI Project Settings --> SSH Keys > Additional SSH Keys, and paste the paste the SSH key.
* If done successfully, if will generate a fingerprint.
### Step 6. Add a new Job in the CircleCI Config file ```configure_infrastructure```
* Add ```configure_infrastructure``` job that uses Ansible to execute your Playbook to configure the EC2 instance.
* ```configure_infrastructure``` job should do the following:
    - run on the ```python:3.7-alpine3.11``` Docker image
    - checkout the repo code to the CircleCI conatiner
    - add the SSH keys from the CircleCI project settings to the CircleCI container
    - install ansible using the command
        ```
        apk add --update ansible
        ```
    - configure the EC2 instance in your AWS account using the command
        ```
        ansible-playbook -i [inventory-file] [playbook-file]
        ```
* Add the new job ```configure_infrastructure``` in the workflows section.

> Hint -
    * excute the first job "that creates infra" and comment out the second job 
    * then get ip/dns of the created instance & update your inventory with such ip/dns
    * comment out the first job and excute the second job "that configures infra"

 



# Packer AMI Blueprint

This repository contains a sample Packer tokeniseable template which, after tokenisation, can be used to publish AMIs to your AWS account.

## Tokenisation
The following values need to be replaced in the template before you can execute a Packer build:
* AWS_ACCOUNT_IDS: A list of accounts you want your AMI to be published to besides the origin account of your source AMI
* AWS_SOURCE_AMI: The AMI which we will use as a base for provisioning
* INSTANCE_USER: The default user for the source AMI e.g. centos, ec2-user, ubuntu
* AWS_VPC_ID: The VPC where we will spin up a temporary instance for the AMI baking
* AWS_SUBNET_ID: The subnet where we will spin up a temporary instance for the AMI baking

## Packer Build
To execute the build of this template, you will need [Packer](https://www.packer.io/intro/getting-started/setup.html) installed.

After verifying your installation, simply run the command  ```build -debug -var aws_access_key=${AWS_ACCESS_KEY} -var aws_secret_key=${AWS_SECRET_KEY} BLUEPRINT_BAKE_AMI.json``` where AWS_ACCESS_KEY and AWS_SECRET_KEY are your defined as environment variables for your AWS API keys respectively.

## Things to note
By default, this template installs Docker, docker-compose and a few other yum packages. This will need updating depending on whatever you want to include in your AMI, and if your source AMI is coming from a different OS thus requiring a different install command.

Note also that the AMI by default assumes your source AMI is in the eu-west-1 region, and publishes to 5 other regions.

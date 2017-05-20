# CloudFormation
REAN CloudFormation Candidate Solution

<h2>Objective:</h2>
Use CM tools such as Puppet, Ansible, or Chef to automate the installation of basic Drupal or WordPress. Setup a sample site. Automate the solution using Cloudformation template.

<h2>Deliverable:</h2>
A cloudformation template that accepts user inputs as parameters where applicable ( for example, Admin password). This template should setup VPC, create subnets, launch a CM instance, pull the necessary code (modules, classes, recipes etc) from a GIT repo (or S3), and configure the web instance for basic Drupal or Wordpress setup.

Execution:

Note: --I was unable to use Chef to automate the installation of WordPress; but still managed to install Chef and WordPress as seperate events. I am assuming the end goal was a Chef managed node with a WordPress installation. This was achieved; however I would still like to know which recipes one should leverage to automate the installation of WordPress.

I attempted to edit the default AWS Chef_Wordpress template located here: https://s3-us-east-2.amazonaws.com/cloudformation-templates-us-east-2/WordPress_Chef.template

But experienced issues with AWS's introduction of an RDS DB instance. AWS is essentially removing the default wordpress DB configurations with there own cookbook. See line 411 in atom text editor (/var/chef/chef-repo/cookbooks/wordpress/attributes/aws_rds_config.rb)

I removed this cookbook reference and researched possible solutions, but was still unable to automate an explicit chef wp installation without leveraging RDS.

Solution:
With proper AWS Access ID and Keys enabled on the user's terminal. The cloudformation can be created with the following AWS CLI command:

aws cloudformation create-stack --stack-name VPCWPChef --template-url https://s3-us-west-1.amazonaws.com/rean-pats-bucket/VPC_CHEF_WP_FINAL.json --parameters ParameterKey=CIDRRange,ParameterValue=10.250.0.0 ParameterKey=DBName,ParameterValue=wordpressdb ParameterKey=DBPassword,ParameterValue=admin1234 ParameterKey=DBRootPassword,ParameterValue=admin1234 ParameterKey=DBUser,ParameterValue=admin ParameterKey=InstanceType,ParameterValue=t2.micro ParameterKey=KeyName,ParameterValue=patskey ParameterKey=SSHLocation,ParameterValue=0.0.0.0/0

Template:
The template is located in S3 under the bucket s3://rean-pats-bucket/VPC_CHEF_WP_FINAL.json
It is also located in this repository under the name: VPC_CHEF_WP_FINAL.json



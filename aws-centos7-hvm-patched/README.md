# aws-centos7-hvm-patched

This Packer template uses one of the official Marketplace CentOS 7 HVM AMIs as it's source and generates a new AMI with the following:

* Runs yum update to fully patch the system.

## Other important variations from the Marketplace AMI
This template sets the default EBS volume type to 'gp2' and delete on instance terminiation to 'true'.

## Variables:
* aws_region: The AWS region where the AMI should be generated. Example: us-west-2
* source_ami_id: The ami id of a CentOS 6.x HVM AWS Marketplace image. Example: ami-af4333cf
* dest_ami_name: The name you would like to give to the resulting AMI. Example: centos7.1-hvm-patched

## Usage:

* Install Packer: https://www.packer.io/downloads.html
* Setup your AWS credentials: https://www.packer.io/docs/builders/amazon.html
* From this directory, execute the following command:

<!-- -->
    
    packer build -var 'aws_region=<aws_region>' -var 'source_ami_id=<source_ami_id>' -var 'dest_ami_name=<dest_ami_name>' aws-centos7-hvm-patched.json 
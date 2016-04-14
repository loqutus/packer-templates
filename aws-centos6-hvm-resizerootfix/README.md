# aws-centos6-hvm-rootvolfix

The CentOS 6.x HVM AMI's in the AWS Marketpace don't resize the root filesystem to the size of the root EBS volume. This Packer template uses one of the official Marketplace CentOS 6 HVM AMIs as it's source and generates a new AMI with the following:

* Enables EPEL. The packages cloud-utils-growpart and dracut-modules-growroot are only available in EPEL.
* Installs cloud-init (if not present), cloud-utils-growpart, and dracut-modules-growroot, which are required for cloud-init to resize the root filesystem when an instance is launched.
* Runs yum update to fully patch the system.
* Runs dracut to generate a new initramfs with the growpart module installed.

## Other important variations from the Marketplace AMI
This template sets the default EBS volume type to 'gp2' and delete on instance terminiation to 'true'.

## Variables:
* aws_region: The AWS region where the AMI should be generated. Example: us-west-2
* source_ami_id: The ami id of a CentOS 6.x HVM AWS Marketplace image. Example: ami-ac5f2fcc
* dest_ami_name: The name you would like to give to the resulting AMI. Example: centos6.7-hvm-growrootfix

## Usage:

* Install Packer: https://www.packer.io/downloads.html
* Setup your AWS credentials: https://www.packer.io/docs/builders/amazon.html
* From this directory, execute the following command:

<!-- -->
    
    packer build -var 'aws_region=<aws_region>' -var 'source_ami_id=<source_ami_id>' -var 'dest_ami_name=<dest_ami_name>' aws-centos6-hvm-resizerootfix.json 
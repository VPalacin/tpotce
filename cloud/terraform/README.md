# T-Pot Terraform
<<<<<<< HEAD

This [Terraform](https://www.terraform.io/) configuration can be used to provision a T-Pot instance in AWS in addition to all of the necessary pre-requisites. Specifically, the following resources will be created:

* EC2 instance:
  * t3.large (2 vCPU, 8 GiB RAM)
  * 128GB disk
  * [Debian Stretch](https://wiki.debian.org/Cloud/AmazonEC2Image/Stretch) (The T-Pot installation script will then upgrade this to Debian Sid)
* AWS Security Group:
  * TCP/UDP ports <= 64000 open to the Internet
  * TCP ports 7012, 7014 and 7017 open to a chosen administrative IP

[Cloud-init](https://cloudinit.readthedocs.io/en/latest/) is used to bootstrap the instance and install T-Pot on startup. Additional provisioning using Ansible etc. is not required.

The following resources are NOT automatically created and need to be specified in the configuration below:

* VPC
* Subnet

## Pre-Requisites

* [Terraform](https://www.terraform.io/) 0.12
* AWS Account
  * Existing VPC. VPC ID should be specified in configuration below
  * Existing subnet. Subnet ID should be specified in configuration below
* AWS Authentication credentials should be [set using environment variables](https://www.terraform.io/docs/providers/aws/index.html#environment-variables)

## Required Configuration Changes

### Terraform Variables

In `aws/variables.tf`, change the following variables to correspond to your existing EC2 infrastructure:

* `admin_ip` - source IP address(es) that you will use to administer the system. Connections to TCP ports 7012, 7014 and 7017 will be allowed from this IP only. Multiple IPs or CIDR blocks can be specified in the format: `["127.0.0.1/32", "192.168.0.0/24"]`
* `ec2_vpc_id`
* `ec2_subnet_id`
* `ec2_region`

### Admin Credentials

In `tpot.conf`, change the following variables:

```
myCONF_WEB_USER='webuser'
myCONF_WEB_PW='w3b$ecret'
```

This will be used to configure credentials for the T-Pot Kibana interface. Refer to [Options](https://github.com/dtag-dev-sec/tpotce#options) for more information.

## Initialising

=======
This [Terraform](https://www.terraform.io/) configuration can be used to launch a virtual machine, bootstrap any dependencies and install T-Pot in a single step.  
Configuration for Amazon Web Services (AWS) and Open Telekom Cloud (OTC) is currently included.
This can easily be extended to support other [Terraform providers](https://www.terraform.io/docs/providers/index.html).

[Cloud-init](https://cloudinit.readthedocs.io/en/latest/) is used to bootstrap the instance and install T-Pot on startup.

# Table of Contents
- [What get's created](#what-created)
  - [Amazon Web Services (AWS)](#what-created-aws)
  - [Open Telekom Cloud (OTC)](#what-created-otc)
- [Pre-Requisites](#pre)
  - [Amazon Web Services (AWS)](#pre-aws)
  - [Open Telekom Cloud (OTC)](#pre-otc)
- [Terraform Variables](#variables)
  - [Common configuration items](#variables-common)
  - [Amazon Web Services (AWS)](#variables-aws)
  - [Open Telekom Cloud (OTC)](#variables-otc)
- [Initialising](#initialising)
- [Applying the Configuration](#applying)
- [Connecting to the Instance](#connecting)

<a name="what-created"></a>
## What get's created

<a name="what-created-aws"></a>
### Amazon Web Services (AWS)
* EC2 instance:
  * t3.large (2 vCPUs, 8 GB RAM)
  * 128 GB disk
  * Debian 10
  * Public IP
* Security Group:
  * TCP/UDP ports <= 64000 open to the Internet
  * TCP ports 7012, 7014 and 7017 open to a chosen administrative IP

<a name="what-created-otc"></a>
### Open Telekom Cloud (OTC)
* ECS instance:
  * s2.medium.8 (1 vCPU, 8 GB RAM)
  * 128 GB disk
  * Debian 10
  * Public EIP
* Security Group
* Network, Subnet, Router (= Virtual Private Cloud [VPC])

<a name="pre"></a>
## Pre-Requisites
* [Terraform](https://www.terraform.io/) 0.12

<a name="pre-aws"></a>
### Amazon Web Services (AWS)
* AWS Account
  * Existing VPC: VPC ID needs to be specified in `aws/variables.tf`
  * Existing subnet: Subnet ID needs to be specified in `aws/variables.tf`
  * Existing SSH key pair: Key name needs to be specified in `aws/variables.tf`
* AWS Authentication credentials should be [set using environment variables](https://www.terraform.io/docs/providers/aws/index.html#environment-variables)

<a name="pre-otc"></a>
### Open Telekom Cloud (OTC)
* OTC Account
  * Existing SSH key pair: Key name needs to be specified in `otc/variables.tf`
* OTC Authentication credentials (Username, Password, Project Name, User Domain Name) can be set in the `otc/clouds.yaml` file

<a name="variables"></a>
## Terraform Variables

<a name="variables-common"></a>
### Common configuration items
These variables exist in `aws/variables.tf` and `otc/variables.tf` respectively.  
Settings for cloud-init:  
* `timezone` - Set the Server's timezone
* `linux_password`- Set a password for the Linux Operating System user (which is also used on the Admin UI)

Settings for T-Pot:  
* `tpot_flavor` - Set the flavor of the T-Pot (Available flavors are listed in the variable's description)
* `web_user` - Set a username for the T-Pot Kibana Dasboard
* `web_password` - Set a password for the T-Pot Kibana Dashboard

<a name="variables-aws"></a>
### Amazon Web Services (AWS)
In `aws/variables.tf`, you can change the additional variables:
* `admin_ip` - source IP address(es) that you will use to administer the system. Connections to TCP ports 7012, 7014 and 7017 will be allowed from this IP only. Multiple IPs or CIDR blocks can be specified in the format: `["127.0.0.1/32", "192.168.0.0/24"]`
* `ec2_vpc_id` - Specify an existing VPC ID
* `ec2_subnet_id` - Specify an existing Subnet ID
* `ec2_region`
* `ec2_ssh_key_name` - Specify an existing SSH key pair
* `ec2_instance_type`

<a name="variables-otc"></a>
### Open Telekom Cloud (OTC)
In `otc/variables.tf`, you can change the additional variables:
* `availabiliy_zone`
* `flavor`
* `key_pair` - Specify an existing SSH key pair
* `image_id`
* `volume_size`  
Furthermore you can configure the naming of the created infrastructure (per default everything gets prefixed with "tpot-", e.g. "tpot-router").

<a name="initialising"></a>
## Initialising
>>>>>>> be1a90524a9a12693fd2f46c2f7fc1bc18825bfe
The [`terraform init`](https://www.terraform.io/docs/commands/init.html) command is used to initialize a working directory containing Terraform configuration files.

```
$ cd aws
$ terraform init
<<<<<<< HEAD

Initializing the backend...

Initializing provider plugins...
- Checking for available provider plugins...
- Downloading plugin for provider "aws" (terraform-providers/aws) 2.16.0...

The following providers do not have any version constraints in configuration,
so the latest version was installed.

To prevent automatic upgrades to new major versions that may contain breaking
changes, it is recommended to add version = "..." constraints to the
corresponding provider blocks in configuration, with the constraint strings
suggested below.

* provider.aws: version = "~> 2.16"

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

## Applying the Configuration

=======
```
OR
```
$ cd otc
$ terraform init
```

<a name="applying"></a>
## Applying the Configuration
>>>>>>> be1a90524a9a12693fd2f46c2f7fc1bc18825bfe
The [`terraform apply`](https://www.terraform.io/docs/commands/apply.html) command is used to apply the changes required to reach the desired state of the configuration, or the pre-determined set of actions generated by a [`terraform plan`](https://www.terraform.io/docs/commands/plan.html) execution plan.

```
$ terraform apply
<<<<<<< HEAD

An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_instance.tpot will be created
  ...

  # aws_security_group.tpot will be created
  ...

Plan: 2 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value:
```

This will perform the following actions:

1. Create EC2 security group
2. Start a Debian EC2 instance
3. Update all packages and reboot if necessary
4. Install T-Pot and required dependencies
5. Reboot

## Connecting to the Instance

### SSH

Prior to the final reboot, you will temporarily be able to SSH to port 22 as per standard. Following the reboot, port 22 is used for the honeypot. The *real* SSH server is listening on port **7014**

### Browser

https://www.example.com:7017/

Replace with the FQDN of your EC2 instance. Refer to the [T-POT documentation](https://github.com/dtag-dev-sec/tpotce#ssh-and-web-access) for further details.
=======
```
This will create your infrastructure and start a Cloud Server. On startup, the Server gets bootstrapped with cloud-init and will install T-Pot. Once this is done, the server will reboot.

If you want the remove the built infrastructure, you can run [`terraform destroy`](https://www.terraform.io/docs/commands/destroy.html) to delete it.

<a name="connecting"></a>
## Connecting to the Instance
When the installation is completed, you can proceed with connecting/logging in to the T-Pot according to the [documentation](https://github.com/dtag-dev-sec/tpotce#ssh-and-web-access).
>>>>>>> be1a90524a9a12693fd2f46c2f7fc1bc18825bfe

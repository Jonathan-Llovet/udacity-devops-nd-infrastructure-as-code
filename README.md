# Udagram - Udacity DevOps Engineer Nanodegree

This is the second project in the Udacity DevOps Engineer Nanodegree Program.

Two AWS Cloudformation templates are used to deploy a web application that scales automatically to meet service demands and is highly available, with redundancy by design to protect against loss of service when there are issues with an AWS availability zone.

The architecture is designed with security in mind. The web servers are placed inside of private subnets that only expose web traffic through a load balancer that acts as a gateway. They also only allow remote administration through intermediary bastion hosts (a.k.a. jump hosts) that require specific ssh keys to grant access. Otherwise, the web servers are inaccessible to the outside world. 

On top of this, all of the infrastructure can be easily created and destroyed. The networking infrastructure is defined separately from the web server infrastructure and can be extended or repurposed to meet similar requirements. Likewise, the server infrastructure can be slightly modified to easily support other web applications. 

Instructions for creating, deleting, and testing the infrastructure can be found below.

## Architecture

![Architecture Diagram](https://github.com/Jonathan-Llovet/udacity-devops-nd-infrastructure-as-code/blob/master/diagram/Project-2-Udagram-Udacity-DevOps-Engineer-Nanodegree.svg)

## Usage

### Prerequisites

- Have an AWS Account with sufficient permissions to create networking and server resources. [Need to create an account?](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/). Note: Some of the features here will not be covered by the AWS free tier. Destroy or stop any unused resources to avoid usage costs.
- If you want to ssh into the instances, create ssh keys and add the names in `udagram-servers-parameters.json`.
- [Install the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html) to manage resources from the command line. 

### Creating the stacks
There are two stacks needed for the application. To deploy the stacks, you can use the following commands to provision them.

Full documentation on the aws cloudformation cli is available [here](https://docs.aws.amazon.com/cli/latest/reference/cloudformation/index.html).

#### Create the networking stack

```SHELL
aws cloudformation create-stack \
--stack-name udagram-network \
--template-body file://udagram-network.yml \
--parameters file://udagram-network-parameters.json \
--region=us-east-1
```

#### Create the servers stack

- This creates IAM Policies, Roles, and Instance Profiles, which require explicit acknowledgement through the `--capabilities` flag to create on the CLI.

```SHELL
aws cloudformation create-stack \
--stack-name udagram-servers \
--template-body file://udagram-servers.yml \
--parameters file://udagram-servers-parameters.json \
--region=us-east-1 \
--capabilities CAPABILITY_NAMED_IAM
```

### Deleting the stacks
When you are finished with the stacks and want to delete them, you can use the following commands.

```SHELL
delete-stack \
--stack-name udagram-network \
```

```SHELL
delete-stack \
--stack-name udagram-servers \
```

### Connecting securely to web servers through bastion hosts for troubleshooting
One way to connect securely the web servers is by using SSH Agent forwarding, which allows you to connect to the web server with the bastion host without copying your ssh key to the bastion host directly, which prevents your web servers from being compromised if your bastion host is hacked.

- [Handling Bastion Hosts on AWS via SSH Agent Forwarding](https://medium.com/@crishantha/handing-bastion-hosts-on-aws-via-ssh-agent-forwarding-f1d2d4e8622a)
- [ssh-add documentation](https://linux.die.net/man/1/ssh-add)

# Udagram - Udacity DevOps Engineer Nanodegree

This is the second project in the Udacity DevOps Engineer Nanodegree Program.

Two AWS Cloudformation templates are used to deploy a web application that scales automatically to meet service demands and is highly available, with redundancy by design to protect against loss of service when there are issues with an AWS availability zone.

It is built with security in mind. The web servers are placed inside of private subnets that only expose web traffic through a load balancer that acts as a gateway. They also only allow remote administration through intermediary bastion hosts (a.k.a. jump hosts) that require specific ssh keys to grant access. Otherwise, the web servers are inaccessible to the outside world. 

On top of this, all of the infrastructure can be easily created and destroyed. The networking infrastructure is defined separately from the web server infrastructure and can be extended or repurposed to meet similar requirements. Likewise, the server infrastructure can be slightly modified to easily support other web applications. 

Instructions for creating, deleting, and testing the infrastructure can be found below.

## Architecture

![Architecture Diagram](https://github.com/Jonathan-Llovet/udacity-devops-nd-infrastructure-as-code/blob/master/diagram/Project-2-Udagram-Udacity-DevOps-Engineer-Nanodegree.svg)

## Usage

### Prerequisites

### Creating a stack

### Connecting securely to web servers through bastion hosts for troubleshooting

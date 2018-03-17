<<<<<<< HEAD
# AWS CloudFormation Starter Playbook

## Introduction

This repository provides a starter template for getting started creating AWS infrastructure using Ansible and CloudFormation.

## Prerequisites

To run this playbook on your local machine, you must install the following prerequisites:

- Ansible 2.4 or higher
- Python PIP package manager
- The following PIP packages:
  - awscli
  - boto3
  - netaddr
- jq

You must also configure your local environment with your AWS credentials and you will also need to specify the ARN of the IAM role that your playbook will use to run provisioning tasks.  Your credentials must have permissions to assume this role.

### macOS Environments

On macOS environments it is recommended that you use the Homebrew package manager to install the most recent version of Python 2.7.

See [brew.sh](http://brew.sh) for details on how to install Homebrew.

Once Homebrew is installed you can install the latest version of Python 2.7 as follows:

```bash
$ brew install python2
...
...
```

This will install the PIP package manager as `pip2` and you can install Ansible and required dependencies:

```bash
$ pip2 install ansible awscli boto3 netaddr
...
...
```

Note that `boto3` must also be installed in the system python, which you can perform as follows:

```bash
$ sudo -H /usr/bin/python -m easy_install pip
...
...
$ sudo -H /usr/bin/python -m pip install boto3 --ignore-installed six
...
...
```

Once you have installed `boto3` in your system python, it is recommended to run the following commands to ensure your Homebrew and system python environments are configured correctly:

```
$ brew unlink python
...
$ brew link --overwrite python
...
```

## Getting Started

1. Fork this repository to your own new repository
2. Review [`roles/requirements.yml`](./roles/requirements.yml) and modify if required
3. Install roles by running `make roles` (which executes `ansible-galaxy install -r roles/requirements.yml`)
4. Define environments in the [`inventory`](./inventory) file and [`group_vars`](./group_vars) folder.  Alternatively you can use the `make environment/<environment-name>` command.
5. Define a CloudFormation stack name in [`group_vars/all/vars.yml`](./group_vars/all/vars.yml) using the `Stack.Name` variable
6. Add the ARN of the IAM role to assume in each environment by configuring the `Sts.Role` variable in `group_vars/<environment>/vars.yml`
7. Define your CloudFormation template in [`templates/stack.yml.j2`](./templates/stack.yml.j2).  Alternatively you can reference a template included with the `aws-cloudformation` role by setting the `Stack.Template` variable to the path of the template relative to the `aws-cloudformation` role folder (e.g. `Stack.Template: templates/network.yml.j2`)
8. Define environment-specific configuration settings as required in `group_vars/<environment>/vars.yml`
9. If you have stack inputs, define them using the syntax `Stack.Inputs.<Parameter>` in your environment settings file (e.g. `Stack.Inputs.MyInputParam: some-value`)
10. Deploy your stack by running `make deploy/<environment>` (which executes `ansible-playbook site.yml -e env=<environment>`)

## Conventions

- Environment specific settings should always be formatted `Config.<Parameter>` (e.g. `Config.VpcName`), unless you have environment specific settings for variables related to the [`aws-sts`](https://github.com/docker-production-aws/aws-sts) or [`aws-cloudformation`](https://github.com/docker-production-aws/aws-cloudformation) roles as defined below

- Variables related to configuring the [`aws-sts`](https://github.com/docker-production-aws/aws-sts) role are formatted `Sts.<Parameter>` (e.g. `Sts.Role`)

- Variables related to configuring the [`aws-cloudformation`](https://github.com/docker-production-aws/aws-cloudformation) role formatted `Stack.<Parameter>` (e.g. `Stack.Name`)
=======
# Docker in Production using AWS - Microtrader Deployment Playbook

This repository provides an Ansible playbook and CloudFormation template for deploying the Microtrader application into an AWS development and production environment, as described in the Pluralsight course [Docker in Production using Amazon Web Services](https://app.pluralsight.com/library/courses/docker-production-using-amazon-web-services/table-of-contents).

## Quick Start

See the [AWS Starter repository README](https://github.com/docker-production-aws/aws-starter) for instructions on how to work with this repository.

## Branches

This repository contains two branches:

- [`master`](https://github.com/docker-production-aws/microtrader-deploy/tree/master) - represents the initial starting state of the repository as viewed in the course.  Specifically this is an empty repository that you are instructed to create in the module **Defining ECS Applications using Ansible and CloudFormation**.

- [`final`](https://github.com/docker-production-aws/microtrader-deploy/tree/final) - represents the final state of the repository after completing all configuration tasks as described in the course material.

> The `final` branch is provided as a convenience in the case you get stuck, or want to avoid manually typing out large configuration files.  In most cases however, you should attempt to configure this repository by following the course material.

To clone this repository and checkout a branch you can simply use the following commands:

```
$ git clone https://github.com/docker-production-aws/packer-ecs.git
...
...
$ git checkout final
Switched to branch 'final'
$ git checkout master
Switched to branch 'master'
```

## Repository Timeline

The following provides links to commits in this repository that represent important milestones in the course material:

- [Defining ECS Applications using Ansible and CloudFormation](https://github.com/docker-production-aws/microtrader-deploy/tree/defining-ecs-applications) - this commit represents the state of the repository once you have completed the Defining ECS Applications using Ansible and CloudFormation module.  This module establishes the supporting infrastructure for the Microtrader application.

- [Microtrader First Deploy](https://github.com/docker-production-aws/microtrader-deploy/tree/microtrader-first-deploy) - this commit represents the state of the repository at the point you perform the first deployment of the Microtrader stack in the Deploying ECS Applications using Ansible and CloudFormation module.

- [Deploying ECS Applications using Ansible and CloudFormation](https://github.com/docker-production-aws/microtrader-deploy/tree/deploying-ecs-applications) - this commit represents the state of the repository once you have completed the Deploying ECS Applications using Ansible and CloudFormation module.  This module establishes the EC2 container service elements of the Microtrader application.

- [Creating CloudFormation Custom Resources using AWS Lambda](https://github.com/docker-production-aws/microtrader-deploy/tree/creating-custom-resources) - this commit represents the state of the repository once you have completed the Creating CloudFormation Custom Resources using AWS Lambda module.

- [Managing Secrets in AWS](https://github.com/docker-production-aws/microtrader-deploy/tree/managing-secrets-in-aws) - this commit represents the state of the repository once you have completed the Managing Secrets in AWS module.

- [Managing ECS Infrastructure Lifecycle](https://github.com/docker-production-aws/microtrader-deploy/tree/managing-ecs-infrastructure-lifecycle) - this commit represents the state of the repository once you have completed the Managing ECS Infrastructure Lifecycle module.

- [Auto Scaling ECS Applications](https://github.com/docker-production-aws/microtrader-deploy/tree/autoscaling-ecs-applications) - this commit represents the state of the repository once you have completed the Auto Scaling ECS Applications module.

- [Continuous Delivery using CodePipeline](https://github.com/docker-production-aws/microtrader-deploy/tree/continuous-delivery-codepipeline) - this commit represents the state of the repository once you have completed the Continuous Delivery using CodePipeline module.

## Errata

No known issues.

## Further Reading

- [CloudFormation User Guide](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)
- [CloudFormation Template Reference](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html)
>>>>>>> c3a5f6964828ca8aec0d18407c59aea4cad9dc16

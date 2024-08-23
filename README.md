# Ansible Playbook to Install Terraform

This repository contains an Ansible playbook designed to install Terraform on Ubuntu servers and initialize a VPC resource. The playbook performs all the necessary steps to ensure Terraform is installed, configured, and ready to manage infrastructure on AWS.

## Playbook Overview

The playbook (`playbook.yaml`) performs the following tasks:

1. Updates the apt package list on Ubuntu.
2. Installs required packages such as `gnupg`, `software-properties-common`, and `wget`.
3. Downloads and adds the HashiCorp GPG key.
4. Verifies the GPG key's fingerprint.
5. Adds the official HashiCorp repository to your system.
6. Updates the package information from the new repository.
7. Installs Terraform.
8. Verifies the Terraform installation.
9. Creates a Terraform project directory.
10. Uploads the Terraform configuration file (`aws-vpc.tf`) into the project directory.
11. Initializes the Terraform directory.
12. Formats Terraform files.
13. Validates the Terraform configuration.

## Terraform Configuration

The Terraform configuration (`main.tf`) sets up an AWS VPC resource with the following parameters:

```hcl
terraform {
  required_version = "~> 1.0"
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
  region  = "us-west-2"
}

resource "aws_vpc" "main" {
  cidr_block       = "10.0.0.0/16"
  instance_tenancy = "default"

  tags = {
    Name = "project-vpc"
  }
}

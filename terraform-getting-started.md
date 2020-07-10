# Getting Started with Terraform

## Introduction

Terraform is the most popular language for defining and provisioning infrastructure as code (IaC). This guide will show you how to install Terraform and use it to provision an AWS resource.

When you finish with this guide, you will have learned to:

- Download and install Terraform
- Create a Terraform configuration
- Initialize and provision an AWS resource

## Prerequisites

Terraform Enterprise runs on Linux instances, and you must prepare a running Linux instance for Terraform Enterprise before running the installer. You will start and manage this instance like any other server.

We provide OS and Hardware requirements below. For a complete list of requirements, see the [Terraform Installation Prerequisites](https://www.terraform.io/docs/enterprise/before-installing/index.html).

**Operating System Requirements:**
- Debian 7.7+
- Ubuntu 14.04.5 / 16.04 / 18.04
- Red Hat Enterprise Linux 7.4 - 7.8
- CentOS 6.x / 7.4 - 7.8
- Amazon Linux 2014.03 / 2014.09 / 2015.03 / 2015.09 / 2016.03 / 2016.09 / 2017.03 / 2017.09 / 2018.03 / 2.0
- Oracle Linux 7.4 - 7.8

**Hardware Requirements:**
- At least 40GB of disk space on the root volume
- At least 8GB of system memory
- At least 2 CPU cores

## Downloading and Installing Terraform

The first step is to download the Terraform software.

To download Terraform, visit [Terraform.io](https://www.terraform.io/downloads.html) and click the appropriate download link for your operating system. This will download a zip file containing a single binary. Install Terraform by unzipping this file and moving it to a directory included in your system's `PATH`.

## Creating Infrastructure

Once Terraform is installed you can begin creating some infrastructure.

We recommend creating a new directory on your local machine and creating Terraform configuration code inside of it. Open a Linux shell and run the following commands:

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

Next, create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

Paste the following lines into the file.

```hcl
provider "docker" {
    host = "unix:///var/run/docker.sock"
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}

resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

Initialize Terraform with the `init` command. This installs the AWS provider. 

```shell
$ terraform init
```

Check for any errors. If the initialization was successful, provision the resource with the `apply` command.

```shell
$ terraform apply
```
*The previous command may take a few minutes to run. Once it finishes, you will see a message indicating that the resource was created.*



Finally, destroy the infrastructure.

```shell
$ terraform destroy
```

Look for a message at the bottom of the output asking for confirmation. Type "yes" and hit ENTER. Terraform will destroy the resources it had created earlier.

## Next Steps

In this guide, you learned how to download and install Terraform, and how to manually initialize an AWS resource. The next guide will show you [How to Run Terraform in Automation](https://learn.hashicorp.com/terraform/development/running-terraform-in-automation).

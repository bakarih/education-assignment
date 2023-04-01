# Getting Started with Terraform

Terraform is the most popular language for defining and provisioning infrastructure as code (IaC).

In this tutorial you will install terraform and verify it's installation by creating a Docker container locally
and running some code against it.

# Prerequisites

* Basic understanding of CLI commands.
* This guide is appropriate for those with beginner-level understanding of Terraform.

# Installing Terraform

To install Terraform, visit [Terraform.io](https://www.terraform.io/downloads.html) and download the binary file for your operating system (OS).

With Terraform installed, let's dive into it and create some infrastructure.

Hashicorp recommends creating a new directory on your local machine and creating Terraform configuration code inside.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```
<img width="419" alt="Screen Shot 2023-03-31 at 5 50 29 PM" src="https://user-images.githubusercontent.com/5651136/229257473-9ff51ca5-34d8-4a19-bc36-590339bba59d.png">


# Creating a file

Next, create a file for your Terraform configuration code.

```shell
$ touch main.tf
```
<img width="456" alt="Screen Shot 2023-03-31 at 5 51 59 PM" src="https://user-images.githubusercontent.com/5651136/229257540-d67cff9f-4762-426c-a0c3-ba00c7db7d01.png">

# Copying Code

Paste the following lines into the file.

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}
provider "docker" {
    host = "unix:///var/run/docker.sock"
}
resource "docker_container" "nginx" {
  image = docker_image.nginx:latest
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

# Initializing Terraform

Initialize Terraform with the `init` command to install the AWS provider. 

```shell
$ terraform init
```
<img width="566" alt="Screen Shot 2023-03-31 at 6 08 44 PM" src="https://user-images.githubusercontent.com/5651136/229258422-dbfebb61-9691-4840-a213-13fea852a727.png">


Check for any errors. If it runs successfully, provision the resource with the `apply` command.

```shell
$ terraform apply
```

<img width="585" alt="Screen Shot 2023-03-31 at 6 25 58 PM" src="https://user-images.githubusercontent.com/5651136/229259120-4cbf2f2b-a916-4f2c-8a13-623a93ac59f4.png">


Then, wait a few minutes for the command to run. Afterward, you will see a message indicating that the command created the resource.

# Cleanup, Cleanup...

Finally, destroy the infrastructure.

```shell
$ terraform destroy
```
<img width="589" alt="Screen Shot 2023-03-31 at 6 27 28 PM" src="https://user-images.githubusercontent.com/5651136/229259175-a76caf77-fc1f-43e1-bb1d-c4aec1206e0f.png">


Look for a message are the bottom of the output asking for confirmation. Type `yes` and hit ENTER. Terraform will destroy the resources it had created earlier.

# Next Steps



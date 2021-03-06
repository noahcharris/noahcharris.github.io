---
layout: post
title:  "Automating with Terraform and Packer"
date:   2017-6-29 16:16:01 -0600
categories: jekyll update
---


Goodbye physics (tentatively), cyberbird bout to fly right out this. Now that I'm applying for jobs in the bay, I'm going to try and resuscitate my project Egora and modernize it using infrastructure tools like Terraform, Docker, and Packer.

Egora is a sprawling single page application that I wrote in 2014-2015 after graduating from Hack Reactor and being silly enough to want to try a startup. It's hosted on AWS. I run a Node.js application server and some worker processes on an AWS EC2 instance. I also use AWS S3/RDS/Route 53 for static, database hosting, and domain stuff respectively. 

I like to think of the idea as a combination of reddit and google maps (but I used OpenStreetMap instead I think) I used Leaflet for the mapping library. It's meant to geographize conversations by allowing users to filter groups by both topic (like a subreddit) and location (i.e. India, Miami, "{ your hometown }"). I think this would be an interesting way to scope internet discourse.

Egora screenshot in landing configuration:

![Egora Landing Configuration]({{ site.url }}/assets/egora_screenshot.jpg)

Ok, so as well as rehosting it, I'm going to use the Docker/Packer/Terraform trifecta to completely automate the deployment process at every step of the way... uh here we go. So I first a folder called agora-deployment where I'm going to store all my infrastructure scripts and files.



## Terraform

Terraform automates infrastructure deployment, it can plug into many services. We're using AWS here. It's actually pretty simple, the guide on their site is really good. Here is the sample configuration file that we will use.

example.tf
```
provider "aws" {
  access_key = "ACCESS_KEY_HERE"
  secret_key = "SECRET_KEY_HERE"
  region     = "us-west-1"
}

resource "aws_instance" "example" {
  ami           = "ami-2757f631"
  instance_type = "t2.micro"
}
```

Now just insert the AWS keys and you are good to go. NEVER let this file anywhere near version control. I once had $6000 charged to my account because I accidentally put these on github. I managed to resolve the issue with an Amazon rep, but that ish is hella scary.

Then we just cd to the directory with the configuration file and run various terraform commands to plan/create/modify/destory infrastructure! Pretty cool. We just keep adding resource blocks to our code to create more infrastructure, and we can even reference between resources using interpolation like so

```
resource "aws_eip" "ip" {
  instance = "${aws_instance.example.id}"
}
```

Terraform has some cool advanced features too,,,,,,,TODO,,,,,,,,,


....use Terraform to build infrastructure on AWS including an EC2 instance built from a Packer image. After it's loaded this Packer image will also provision (run some code) to initialize the server.

Here is the example packer build file from their documentation:

```
{
  "variables": {
    "aws_access_key": "",
    "aws_secret_key": ""
  },

  "builders": [{
    "type": "amazon-ebs",
    "access_key": "{{user `aws_access_key`}}",
    "secret_key": "{{user `aws_secret_key`}}",
    "region": "us-east-1",
    "source_ami_filter": {
      "filters": {
      "virtualization-type": "hvm",
      "name": "*ubuntu-xenial-16.04-amd64-server-*",
      "root-device-type": "ebs"
      },
      "owners": ["099720109477"],
      "most_recent": true
    },
    "instance_type": "t2.micro",
    "ssh_username": "ubuntu",
    "ami_name": "packer-example {{timestamp}}"
  }],

  "provisioners": [{
    "type": "shell",
    "inline": [
      "sleep 30",
      "sudo apt-get update",
      "sudo apt-get install -y redis-server"
    ]
  }]

}
```












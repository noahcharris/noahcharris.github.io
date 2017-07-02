---
layout: post
title:  "Dockerizing Egora"
date:   2017-7-2 16:16:01 -0600
categories: jekyll update
---



## Docker and Packer

Let's zoom out a bit. Remember that Egora's server has a main serving process and then various worker processes. One of our ultimate goals alongside automating infrastucture is to make horizontal scaling like this much more elegant and modular. This is where Docker comes in, because Docker can package each of the services into its own environment with all needed dependencies. For instance, one of the Egora services uses RabbitMQ for a queue, another uses memcached (or Redis I forget). Then instead of having a mess of software all on one machine, the services are neatly organized and become very convenient and modular. These Docker 'containers' have a small footprint compared to virtual machines and so Docker lends itself to massive and artful horizontal scaling.

But we need something to control Docker, which is where Packer comes in. Packer is the software we use to build the machine images we will be loading with Terraform. Packer also does something called 'provisioning' which just means running code to initialize the server after the image is up and running. So here is the outline of our automation:

Use Terraform to build infrastructure on AWS including an EC2 instance built from a Packer image. After it's loaded this Packer image will also provision (run some code) to pull all our services via Docker and initialize them.


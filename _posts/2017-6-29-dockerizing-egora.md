---
layout: post
title:  "Dockerizing Egora"
date:   2017-6-29 16:16:01 -0600
categories: jekyll update
---


Goodbye physics (tentatively), cyberbird bout to fly right out this. Now that I'm applying for jobs in the bay, I'm going to try and resuscitate my project Egora and modernize it using infrastructure tools like Docker and Packer.

Egora is a sprawling single page application that I wrote in 2014-2015 after graduating from Hack Reactor and being silly enough to want to try a startup. It's hosted on AWS. I run a Node.js application server and some worker processes on an AWS EC2 instance. I also use AWS S3/RDS/Route 53 for static, database hosting, and domain stuff respectively. 

I like to think of the idea as a combination of reddit and google maps (but I used OpenStreetMap instead I think) I used Leaflet for the mapping library. It's meant to geographize conversations by allowing users to filter groups by both topic (like a subreddit) and location (i.e. India, Miami, "{ your hometown }"). I think this would be an interesting way to scope internet discourse.

Egora screenshot in landing configuration.

![Egora Landing Configuration]({{ site.url }}/assets/egora_screenshot.jpg)

Ok, so as well as rehosting it, I'm going to use the Docker/Packer/Terraform trifecta to completely automate the deployment process at every step of the way... uh here we go.











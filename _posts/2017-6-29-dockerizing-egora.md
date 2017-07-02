---
layout: post
title:  "Dockerizing Egora"
date:   2017-6-29 16:16:01 -0600
categories: jekyll update
---
You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `bundle exec jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.




Goodbye physics (tentatively), cyberbird bout to fly right out this. Now that I'm applying for jobs in the bay, I'm going to try and resuscitate my project Egora and modernize it using infrastructure tools like Docker and Packer.

Egora is a sprawling single page application that I wrote in 2014-2015 after graduating from Hack Reactor and being silly enough to want to try a startup. It's hosted on AWS. I run a Node.js application server and some worker processes on an AWS EC2 instance. I also use AWS S3/RDS/Route 53 for static, database hosting, and domain stuff respectively. 

I like to think of the idea as a combination of reddit and google maps. It's meant to geographize conversations by allowing users to filter groups by both topic (like a subreddit) and location (i.e. India, Miami, "{ your hometown }"). I think this would be an intersting way to scope internet discourse.

Here is a screenshot of the project when it was online.
![My helpful screenshot]({{ site.url }}/assets/egora_screenshot.jpg)

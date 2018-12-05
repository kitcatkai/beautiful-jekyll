---
layout: post
title: Transforming GB data using AWS Batch, S3, ElasticBeanStalk and Python library Multiprocessing
image: /img/hello_world.jpeg
---

I hope this blog post can also help those who are tasked to transform huge dataset,in the order of ```GB```, yet they do not have access to huge computing resource locally. 

A brief background of the task I was assigned to, I need to call OSRM, an open-source map matching service, to map match GPS coordinates. Initially, I process the data by calling a python script using library Multiprocessing to retrieve files from AWS s3 and then calling the OSRM API end point, by running OSRM docker container on my local machine. 

However, in the interest of time, I decided to adopt AWS Batch and ElasticBeanStalk to speed up the data transformation process. I first setup AWS ElasticBeanStalk to run my OSRM Docker Container. It can be simple as just uploading your zipped file that contains ```Dockerfile``` and all the relevant files required to build your image. For those productivity-hacker, you can just setup a quick and easy travis webhook that will automatically deploy your container to AWS EBS whenever you ```git push``` your ```Dockerfile```. 

Following the setup of AWS EBS, I run AWS Batch to partition my data as individual calls for my API end point. As such, I can take full advantage of the parallel computing for the data transformation. Even for the partition of my data, I also use python library ```MultiProcessing``` 

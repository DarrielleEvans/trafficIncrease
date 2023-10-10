# Application Traffic Increase

## Purpose

The URL Shortener Application has become very popular recently. The URL Shortener is growing in demand, and you must ensure at least 14,000 users can access the application anytime.
The QA engineer will send 14,000 requests to the server. After the QA engineer tested the application, 8 requests could not access it. As the DevOps engineer,
it's my responsibility to deploy a new version of the application that ensures 14,000 people at a minimum can access the application at once. 


### QA Report
Initial Test: 14000 Request sent to URL Shortener Application
Initial Results: 8 requests were not successful
Summary sent to Devops Engineer: Application Infrastructure does not meet the required simultaneous 14,000 minimum traffic requests.

### Resolution Steps
* The application's infrastructure was initially stored on a t.2 medium EC2. I created a new t.2 xlarge instance which has double the
   vCPU than a t.2 medium.
* Instead of configuring the ec2 with the necessary dependencies all over again, I took a snapshot of the Elastic Block Store Volume located on the 
  t.2 medium instance and detached it.
* Once the t.2 xlarge instance was connected, I attached the volume from the t.2 medium to this instance.
* I then replaced the t.2 xlarge instance's volume with a snapshot of the t.2 medium volume.
* I reran the Jenkins build and accessed the URL Shortener application on port 5000.
  
### Diagram
![Blits2 drawio-2](https://github.com/DarrielleEvans/trafficIncrease/assets/89504317/d5411233-c54f-4559-a07c-27057e192acf)

### Resources
[Detach AWS EBS Volume](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-detaching-volume.html#umount-detach-volume)



# AWS-MultiTier-Architecture
Using EC2 instances to deploy Tomcat, MySQL, RabbitMQ, and Memcached servers; hosted on a Route53 DNS. Incorporates ELB's, SG's, ASG, &amp; S3.


![IMG_A4E47AD91685-1](https://github.com/andreapeterson/AWS-MultiTier-Architecture/assets/134665743/d5e9d2fe-76d8-4c49-8342-1fad851a8d92)


Following the schema above, I deployed a multi-tier web application for no one other than my beloved dog. I am doing a course from the wonderful Imran Teli, so the code above comes mostly from [here](https://github.com/devopshydclub/vprofile-project/tree/aws-LiftAndShift). I edited the 'applications.properties' file so my Tomcat instances can have the addresses for my specific backend servers (that match the Route53 Private Zone records for the backend instances IP addresses) as well as customized the 'welcome.jsp' and images folder to add content specific for my pup. 

To get more specific on a few steps that aren't as apparent in the diagram- I used Maven to build an artifact, then pushed it to an S3 bucket via CLI. The Tomcat instances are attached to an IAM Role, so they have full access to S3. From the Tomcat instance, I copied the artifact from the S3 bucket into /tmp/, stopped Tomcat, removed the default application(/var/lib/tomcat9/webapps/ROOT), copied the artifact to /var/lib/tomcat9/webapps/ROOT.war, then started the Tomcat service. Then, I created an AMI from that instance so it can be used inside a launch template so the ASG's can create instances exactly like it.

This is all done manually, but I am excited to build on this project and add automation as well as soon dive into PAAS & SAAS.

Below is the final project. I checked the HTTPS, database, Memcached, and RabbitMQ.

![Jan-16-2024 20-35-18](https://github.com/andreapeterson/AWS-MultiTier-Architecture/assets/134665743/82cd302e-a881-446b-8181-d4e69dab7210)

![Jan-16-2024 20-36-17](https://github.com/andreapeterson/AWS-MultiTier-Architecture/assets/134665743/c1c1ed8d-7e23-4aff-bec7-0c3188c13858)

# AWS-MultiTier-Architecture
Using EC2 instances to deploy Tomcat, MySQL, RabbitMQ, and Memcached hosted on a Route53 DNS. Incorporates ELB's, SG's, ASG, &amp; S3.

Following the schema above, I deployed a multi-tier web application for no one other than my beloved dog. I am doing a course from the wonderful Imran Teli, so the code above comes mostly from [here](https://github.com/devopshydclub/vprofile-project/tree/aws-LiftAndShift). I edited the 'applications.properties' file so my Tomcat instances can have the addresses for my backend servers (that match the Route53 Private Zone records for the backend instances IP addresses) as well as customized the 'welcome.jsp' and images folder to add content specific for my pup. 

To get more specific on a few steps that aren't as apparent in the diagram- I used Maven to build an artifact, then pushed it to an S3 bucket via CLI. The Tomcat instances are attached to an IAM Role, so they have full access to S3. From the Tomcat instance, I copied the artifact from the S3 bucket into /tmp/, stopped Tomcat, removed the default application(/var/lib/tomcat9/webapps/ROOT), copied the artifact to /var/lib/tomcat9/webapps/ROOT.war, then started the Tomcat service. Then, I created an AMI from this instance so it can be used inside a launch template so the ASG's can create instances exactly like it.

This is all done manually, but I am excited to build on this project and add automation as well as soon dive into PAAS & SAAS. It truly shows the amount of work that goes into manual production and how easy it is to make mistakes.

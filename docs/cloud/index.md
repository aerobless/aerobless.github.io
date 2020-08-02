# AWS Developer Associate

Desired certification: https://aws.amazon.com/certification/certified-developer-associate/

Learning material:

+ https://www.freecodecamp.org/news/pass-the-aws-developer-associate-exam-with-this-free-16-hour-course/
+ https://digitalcloud.training/amazon-aws-free-certification-training-developer-associate/


## Exam Info

+ 72% correct required for pass
+ 65 Questions (18 could be wrong)
+ duration 130min -> 2min per question

### Question Types 

+ Multiple Choice: select 1 out of 4
+ Multiple Responses: select 2 or more out of 5

### Exam breakdown

+ 22% Deployment (14.3 Q)
+ 26% Security (16.9 Q)
+ 30% Development with AWS Services (19.5 Q)
+ 10% Refactoring (6.5 Q)
+ 12% Monitoring and Troubleshooting (7.8 Q)

### Recommended [Whitepapers](https://aws.amazon.com/whitepapers/?whitepapers-main.sort-by=item.additionalFields.sortDate&whitepapers-main.sort-order=desc)

1. Architecting for the Cloud: AWS Best Practices
2. Practicing Continuous Integration and Continuous Delivery on AWS Accelerating Software Delivery with DevOps
3. Microservices on AWS
4. Running Containerized Microservices on AWS
5. Blue/Green Deployments on AWS
6. Serverless Architecture with AWS Lambda
7. Optimizing Enterprise Economics with Serverless Architecture

## Elastic Beanstalk (EB)

**Type:** PaaS
**Does:** Quickly deploy & manage web-apps without worrying about the underlying infrastructure
**Note:** Not recommended for production applications (enterprise, large companies)

 Elastic Beanstalk is powered by CloudFormation templates that set up: Load Balancer, Autoscaling, DB, EC2, Monitoring etc.

 **Supported Languages:** Go, NodeJS (ExpressJS), Java, Ruby (Rails), ASP.NET, Python (Django), PHP (Laravel), Docker

Choose environment: Web vs Worker, typically 1 web + 1 worker
 
current: https://youtu.be/RrKRN9zRBWs?t=1541


### [EB Deployment Policies](https://youtu.be/RrKRN9zRBWs?t=1970)

EB Deployment is In-Place.

+ **All At Once Deployment:** Deploys the new application to all instances at the same time, take all instances out of service while the deployment is executed. Then server become available again. This has downtime. Is fast but dangerous.

+ **Rolling Deployment:** Takes two instances (out of n) down and updates them. The instances are out of service during update. Re-attaches them when they're healthy. No downtime.

+ **Rolling With Additional Batch:** Launch new instances to replace the ones that are taken down for updating. This keeps the same number of instances available to the consumer. There's no reduced capacity.

+ **Immutable:** Creates a new Auto Scaling Group (ASG) with a new EC2 instance in it. Deploys the updated version on the new EC2 instances. Points the elastic load balancer (ELB) to the new ASG and delete the old ASG which terminates the old EC2 instances. For rollback purposes the old ASG and EC2 instance can also be kept until we're sure that we won't need to rollback. This is the safest way to deploy.

| Method | speed | no downtime | no dns change | rollback | failure impact | code deployed |
|-|-|-|-|-|-|-|
| All at once | fast | false | true | manual | downtime | existing |
| Rolling | medium | true | true | manual | single batch out of service, if any were successful mix of old/new | existing |
| Rolling with additional batches | medium | true | true | manual | mix of old/new | existing |
| Immutable | slow | true | true | switch back to old AGS, stop new instance | minimal | new |
| blue/green | slow | true | false | swap url | minimal | new |

DNS changes have to propagate first, which can make it slower

### [In-Place vs. Blue/Green Deployments](https://youtu.be/RrKRN9zRBWs?t=2332)

EB performs In-Place deployments by default. It depends on the scope as to which strategies we consider In-Place.
+ **For EB: All at once, Rolling, Rolling with additional batch, Immutable**
+ For the scope of a server: All at once, Rolling
+ For the scope of an uninterrupted server: Zero-downtime deployments where blue/green occurs on the server itself. E.g. handled by starting new spring boot app on the same server with a different url and having a mechanism to switch over.

**Blue/Green deployments in the context of EB is swapping EB environments and this occurs at DNS level.** If it all happens in the same environment it's not blue/green.

Switching at load balancer level (ELB) is better than at DNS level because with DNS there could be an interruption of service due to DNS propagation. Blue/Green with EB requires that the database is outside of EB envs, because envs are terminated with loss of all their resources.

### EB Configuration files

+ .ebextensions: contains config files (*.config). In .config files we can control: option settings, linux/windows server configs, custom resources.
+ env.yaml: name of environment, solution stack, environment links (connect web + worker), load balancer etc.
+ linux server config: packages to be installed, user groups, users, files on ec2 inline or url, commands to run before application is installed, services (nginx etc.), container commands used our own application: e.g. start-server.py etc.

### [EB CLI](https://youtu.be/RrKRN9zRBWs?t=2989)
Clone repo and install. Basic commands are self-explanatory.

### EB Custom Image
A custom AMI (Amazon Machine Image) is useful if we have a lot of software to install that isn't included in standard AMIs (improves provisioning time).

**Workflow:**

1. AWS Docs to find existing AMIs, one that comes closest to what we want so we can use it as a base
2. CLI -> `describe-platform-version`, get ImageId (of AMI)
3. Got to EC2 marketplace -> community section, paste id to find image
4. Launch new EC2 server, log-in (sessions-manager or ssh)
5. install desired packages and configs
6. bake new AMI, get id of that AMI and use it in our config

### [Configuring RDS (relational database)](https://youtu.be/RrKRN9zRBWs?t=3219)

Can be inside or outside of EB environment. Inside is intended more for developers as the db is terminated if the env is terminated. However with in-place deployments this would work since the environment is never terminated. Outside is intended for productions. The db is created separate from the EB env, so it's not terminated with the environment.




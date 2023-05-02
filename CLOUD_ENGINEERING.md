[IAM]

- IAM is service that manage user and group permission
- Entity in IAM:
    - User
    - Group
    - Policy: is a JSON document describe permission

[EC2]

- EC2 instance types:
    - Class
    - Generation
    - Size

- Type:
    - General purpose
    - For computing 
    - For high memory application
    - For high storage application

[EBS]

- EBS is volume of network that you can attach your instance into.
- EBS can only mount to one instance at a time.
- EBS is bound to AZ
- EBS can be taken as a snaphost and copy across AZ

[AMI]

- AMI: AWS machine image.
- EC2 can be taken as a snapshot and copy across region.

[EC2 Instance Storage]

- EC2 Instance storage is better perfomance alternatives of EBS.
- Multiple EC2 instance can attach to EC2 instance storage.

[ELB]

- ELB: elastic load balancer. 
    + Feature:
        - Integrate with EC2
        - Health check
- Type:
    + Classic LB: old
    + ALB: L7 LB, http, https, websocket
        + Routing base one HTTP header, URL, hostname.
    + NLB: L3 LB
        + Routing base on EC2 instance, IP, ALB
    + GLB: L3 LB
- Sticky session: ALB support session affinity using cookie. 
- Cross zone balancing: with cross zone balancing, request is distributed evenly across multiple EC2 across AZ.

[ASG]

- Important attributes:
    - Min size
    - Max size
    - Initial capacity
- Scale is base on cloud watch alarms, base on metric such as CPU load, Request Count, network, ...
- After scale, ASG have a cool down time before scale up or down again.

[RDS]

- RDS: relational database service.
- Advantage of RDS:
    + Automated provisioning
    + Auto backup
    + Monitoring dashboard.
    + Read replicas
    + Multi AZ setup for DR
    + Auto scaling
- Auto scaling: when storage run out, RDS automatically scale up.
- RDS read replicas up to 5 instance. 
- Autora DB:
    + Up to 15 replicas
    + Auto scale up by 10 GB increment, max to 128 TB.

[VPC]

- VPC: is regional resources.
- VPC is partition into sub nets.
- Each VPC have private and public subnets.
- Internet gateway help VPC connect to internet.
- Public subnet have route to IGW
- Private subnet if want to talk to internet have to talk to public subnet via NAT gateway.
- There are two way to connect VPC:
    + VPC 
    + Direct connect

[S3]

- S3: is a file storage for AWS.
- Bucket in S3 need to have unique name globally.
- Key name in S3 include: prefix + object name.
- S3 can be replicate across region, copy S3 is async.
- S3 object can be moved across storage class.

[CLOUD FRONT]

- CDN network, 126 edge locations.
- DDos protection.
- Origin of CloudFront:
    - S3 bucket
    - Any server: ALB, EC2, S3.
- S3 replication vs cloud front:
    - S3 replication use for dynamic content that need update in realtime.
    - Cloud front is best use for caching static content.
- Cache is base on:
    - Headers
    - Query String parameters
- Dynamic vs static content can be seperated each request.
- To enable cloud front cache server content, origin must have public IP and security group allow cloud front.
- Cloud front access restriction:
    - Using singed URL and signed cookie.

[DOCKER]

- Docker repository:
    - Dockerhub
    - Amazon ECR
- Difference between VM and docker:
    1. VM run on Hypervisor that have it own OS kernel, it takes up resources from host machine (RAM, disk), docker virtualize on application layer, it run on top of OS kernel under docker daemon.
    2. VM is much larger in size than container
    3. Docker have lower initial time to boostraps

- Docker in AWS:
    - ECS: for manage container
    - EKS: for k8s
    - AWS Fargate: serverless container platform
    - AWS ECR: store container image

- Task definitions are meta-data in JSON form to tell ECS how to run docker container

- Launch type of ECS:
    - Add a side car to EC2 instance 
    - Using fargate 

- AWS CES entity:
    - Task: runtime instance
    - Task definition: define resource, docker image, network
    - Cluster: group of task
    - Container
    - Service: managment system for tasks

[SQS]

- SQS: Simple queue services
- Attributes:
    - No throughput limit, no number of messages stored.
    - Retention time: 4 - 14 days, if not processed it will be lost
    - Low latency: 10ms
    - Size: 256 kb
    - ALO delivery.
    - Poll message up to 10 message at the time.
- Queue System processing, consumer need to poll, process then delete message. Consumer process a single message.

[SNS]

- Pub/Sub system, message can be send to multiple subcriber. 

[LAMBDA]

- Function: primary unit of lambda.
- Pros:
    - No need to manage infra
    - Auto-scaling
    - Cost
- Use Cases:
    - API gateway intergation, API gateway + lambda
    - Serverless cron jobs, cloud watch + lambda
    - Event processing with SNS + SQS

[DYNAMODB]

- Dynamo DB is a distributed NoSQL storage, that can automatically replicate data across AZ
- Dynamo DB:
    - Primary key
    - Optionally a sort Key
    - Partion key (hash key)
- Dynamo DB offer:
    - Auto scale
    - Replication
    - Patching
    - Full backup
- Dynamo DB stream:
    - Add an event when add, update or delete an item
- Read consistency type:
    - Eventually consistentcy
    - Strong consistency
- Prioritize read over write when using dynamo DB.
- Scan vs query:
    - Scan equivalent to SELECT * FROM TABLE
    - Scan is very expensive because it scans whole table records, filterExpression will not work in scan function
    - Query: using partition key and range key as input
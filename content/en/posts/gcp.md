---
slug: gcp
title: gcp
date: 2025-10-28 12:07:45
tags:
- google cloud
- google 
categories:
  - Note
---
slug: gcp

# Last-Minute Prep - GCP Competition Notes
[Notes - Concept Clarification](https://hackmd.io/@Eason2392/B1CqW-mkC)

## 2022 Past Exam Questions

### Create VM | VPC

#### create VPC | SubNet | FR | VM | SSH
```=
gcloud compute networks create --help
gcloud compute networks subnets create --help
gcloud compute firewall-rules create --help
gcloud compute instances create --help
gcloud compute ssh --help
```
### Create SQL DB

```=
gcloud compute networks create --help
gcloud compute networks subnets create --help
```
#### Create cloud sql | management instance group

```=
gcloud sql instances --help
gcloud compute instance-templates create --help
gcloud compute instance-groups managed create --help
gcloud compute instance-groups managed set-autoscaling --help
gcloud compute instances add-tags --help
```
##### Firewall rule for health check

```=
gcloud compute firewall-rules create --help
```
##### HTTP load balance

```=
gcloud compute addresses create --help
gcloud compute http-health-checks --help
gcloud compute backend-services create --help
gcloud compute backend-services add-backend url-maps --help 
gcloud compute target-http-proxies create --help 
gcloud compute forwarding-rules create --help 
```

### GCS BUCKET

```=
gcloud builds submit --help
gcloud run deploy --help
```
# 2022 Problem-Solving Walkthrough
## Problem 1

Problem Description:
Tickets for the MeiDei concert will go on sale in a few days. Your friend wants to enjoy the concert with his/her family and urgently needs a pair of tickets. He/She asks you to help set up a machine that will run some magic scripts to automatically purchase tickets as soon as they go on sale. The ticketing system is located in Taiwan, so you should minimize the latency from the machine to the ticketing system while keeping the budget small. To protect this machine, you need to configure it so that only you and your friend (referee-group@taiwan-52nd-national-skills-competition.today) can log in via Cloud Shell or cloud commands. Your environment should have:

- A VPC network named meidei-vpe
- A subnet named meidei-vpc-subnet, location: asia-east1, IP range: 192.168.100.0/24
- Firewall rule name: allow-ssh-only
- VM name: give-me-tickets (2 vCPUs, 4GB RAM, 10GB disk, Debian GNU/Linux 10 (buster), in the meidei-vpe-subnet1 subnet, zone asia-east1)
- Solve this problem using gcloud.

The following is the solution using gcloud:

bash
Copy code
*Create VPC network and subnet*
```=
gcloud compute networks create meidei-vpe --subnet-mode=custom
gcloud compute networks subnets create meidei-vpc-subnet --network=meidei-vpe --region=asia-east1 --range=192.168.100.0/24
```
*Create firewall rule*
```=
gcloud compute firewall-rules create allow-ssh-only --network=meidei-vpe --allow=tcp:22 --source-ranges=[YOUR_IP]/32
```
*Launch the VM*
```=
gcloud compute instances create give-me-tickets --machine-type=n1-standard-2 --zone=asia-east1-a --subnet=meidei-vpc-subnet --image-family=debian-10 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=give-me-tickets
```
*Add SSH access*
```=
gcloud compute instances add-metadata give-me-tickets --metadata=ssh-keys=[USERNAME]:$(cat ~/.ssh/id_rsa.pub)
```
*Allow login via Cloud Shell or cloud command*
```=
gcloud compute instances add-metadata give-me-tickets --metadata=enable-oslogin=TRUE
```
*Add the participant (your friend)*
```=
gcloud projects add-iam-policy-binding [YOUR_PROJECT_ID] --member=group:referee-group@taiwan-52nd-national-skills-competition.today --role=roles/compute.osLogin
```
Please replace [YOUR_IP] and [YOUR_PROJECT_ID] in the commands with your own IP address and project ID.

## Problem 2
Problem Description:
BPM Bakery's business is booming. Due to insufficient service capacity, they are frustrated with their online ordering system. After investigation, they decided to migrate their on-premises system to the cloud. Following discussions, you are responsible for designing an architecture on GCP to serve BPM Bakery's online ordering system. They want the system to provide high availability (capable of handling 2,000 concurrent requests from the same source VM) at low cost. They will provide the source code for their website and a database dump, and you will help them migrate these resources to the cloud environment.
Resources provided by BPM Bakery (your project has read access; these resources are stored in Cloud Storage buckets):
The environment should include:
- A VPC network named bpm-vpe
- A subnet for web servers in Taiwan, named bpm-vpc-subnet1 (10.0.1.0/24).
- A Google-managed SQL database (MySQL 8.0), labeled problem-number: 2 (ensure problem-number: 2 is a user-defined label, not the Cloud SQL instance name), with no external IP and only allowing connections from web servers.
- A managed instance group named bpm-mig in bpm-vpe-subnet1 (zone b):
  - Each instance has no external IP but needs internet connectivity;
  - Normal operational spec for each instance: 2 vCPUs, 4GB RAM, and 10GB Debian GNU/Linux 10 (buster) persistent disk;
  - Capable of scaling in/out based on CPU utilization threshold (60%);
  - Must serve traffic with a minimum of 1 and maximum of 2 instances, with port 80 open to serve web server content.
- An HTTP load balancer named http-lb, with a backend named htip-Ib-be and a frontend named http-ib-fe (use the pre-reserved external IP bpm-external-ip), to load-balance internet traffic to web servers. (For this configuration, note that health checks must be enabled first by creating a firewall rule allowing inbound traffic on port 80 from 130.211.0.0/22 and 35.191.0.0/16 to instances.)

In addition to the resources listed above, you may need to leverage further necessary services to ensure your architecture works correctly.

The following are the steps and explanations for solving the problem using gcloud:

1. **Create VPC network and subnet:**
   ```bash
   gcloud compute networks create bpm-vpe --subnet-mode=custom
   gcloud compute networks subnets create bpm-vpc-subnet1 --network=bpm-vpe --region=asia-east1 --range=10.0.1.0/24
   ```

2. **Create Google-managed SQL database:**
   ```bash
   gcloud sql instances create [INSTANCE_NAME] --database-version=MYSQL_8_0 --region=[REGION] --no-address --labels=problem-number=2
   ```

3. **Create managed instance group:**
   ```bash
   gcloud compute instance-templates create bpm-instance-template --machine-type=n1-standard-2 --subnet=bpm-vpc-subnet1 --tags=bpm-mig --image=debian-10 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=bpm-instance-template
   gcloud compute instance-groups managed create bpm-mig --template=bpm-instance-template --base-instance-name=bpm-instance --size=1 --zone=[ZONE]
   ```

4. **Configure HTTP load balancer:**
   ```bash
   gcloud compute addresses create bpm-external-ip --global
   gcloud compute firewall-rules create allow-health-check --network=bpm-vpe --allow=tcp:80 --source-ranges=130.211.0.0/22,35.191.0.0/16
   gcloud compute health-checks create http bpm-http-health-check --port=80
   gcloud compute backend-services create htip-Ib-be --protocol=HTTP --health-checks=bpm-http-health-check --global
   gcloud compute backend-services add-backend htip-Ib-be --instance-group=bpm-mig --instance-group-zone=[ZONE] --global
   gcloud compute url-maps create bpm-url-map --default-service=htip-Ib-be
   gcloud compute target-http-proxies create http-lb-proxy --url-map=bpm-url-map --global
   gcloud compute forwarding-rules create http-content-rule --address=bpm-external-ip --global --target-http-proxy=http-lb-proxy --ports=80
   ```

These steps will establish the basic infrastructure required to achieve high availability at low cost. Please replace the appropriate variables such as [

## Problem 3
Luxubuuu company is building a smart photo album application for their new business. The application should be built using several microservices, including a website for image uploads and a landmark detection system. They have decided to outsource the static official website hosting and landmark detection system, and you have been entrusted with this task.
You need to make the website accessible from the internet via the reserved IP address luxubuuu-external-ip.
Website source code location (your project has read access; resources are stored in a Cloud Storage bucket):
gs://taiwan-52nd-national-skills-competition-cloud-computing/nsc-q3/website
Additionally, Luxubuuu company wants to upload images through their carefully prepared web UI (uploaded images should be prevented from public access), and retrieve extracted landmark information using a specific API.
They want to adopt a SERVERLESS architecture and will only provide you with two microservice source codes and their respective Dockerfiles: one for image upload and one for retrieving landmark information. In addition to deploying these two Docker images, you are also responsible for building the landmark information extraction service behind the scenes. (Hint: You can use the Google Vision API for this LANDMARKS DETECTION task.)
The provided Docker images are well coded but require you to modify some environment variables: project ID, path to JSON credentials, Cloud Storage bucket name, Firestore collection name, and document name. The client also specifies that requests sent to http://<luxubuuu-external-ip>/internal/upload will use the upload-service, while requests sent to http://<luxubuuu-external-ip>/internal/retrieve will be forwarded to the retrieve-service.
upload-service source code location (your project has read access; resources are stored in a Cloud Storage bucket):
gs://taiwan-52nd-national-skills-competition-cloud-computing/nsc-q3/upload-service
retrieve-service source code location (your project has read access; resources are stored in a Cloud Storage bucket):
gs://taiwan-52nd-national-skills-competition-cloud-computing/nsc-q3/retrieve-service
Note that there is a hard-coded Google Cloud Storage image upload process in the provided upload-service source code. Similarly, there is a hard-coded Firestore in the provided retrieve-service source code.

The following are the steps and corresponding gcloud commands to solve the problem:

1. **Set up static official website hosting**:
```bash
gsutil mb gs://luxubuuu-website
gsutil cp gs://taiwan-52nd-national-skills-competition-cloud-computing/nsc-q3/website/* gs://luxubuuu-website
```

2. **Set up landmark detection service**:
Here we will use the Google Vision API to complete the landmark detection task, a serverless solution.
```bash
gcloud services enable vision.googleapis.com
```

3. **Deploy microservices upload-service and retrieve-service**:
Here we need to modify the environment variables in the Dockerfile, then deploy using Cloud Build.
```bash
gcloud builds submit --tag gcr.io/[PROJECT_ID]/upload-service:v1 .
gcloud builds submit --tag gcr.io/[PROJECT_ID]/retrieve-service:v1 .
```

4. **Deploy Cloud Function to handle landmark information extraction service**:
Here we use Cloud Functions to handle the extraction of landmark information.
```bash
gcloud functions deploy landmark-extraction \
  --runtime=nodejs14 \
  --trigger-http \
  --allow-unauthenticated
```

5. **Configure HTTP load balancer to forward requests**:
```bash
gcloud compute addresses create luxubuuu-external-ip --global
gcloud compute backend-buckets create website-bucket --gcs-bucket-name=luxubuuu-website
gcloud compute backend-services create website-backend-service --global \
    --backend-bucket=website-bucket
gcloud compute url-maps create website-url-map --default-backend-service=website-backend-service
gcloud compute target-http-proxies create website-http-proxy --url-map=website-url-map
gcloud compute forwarding-rules create http-content-rule --address=luxubuuu-external-ip \
    --global --target-http-proxy=website-http-proxy --ports=80
```

This completes the architecture design for building Luxubuuu company's smart photo album application on Google Cloud Platform.
    
## Exam Announcement
The following are gcloud commands related to each topic and how to use them:

1. **Pub/Sub (Queue and Publish/Subscribe)**:
   - **Create a Topic**:
     ```bash
     gcloud pubsub topics create [TOPIC_NAME]
     ```
   - **Subscribe to a Topic (Subscription)**:
     ```bash
     gcloud pubsub subscriptions create [SUBSCRIPTION_NAME] --topic=[TOPIC_NAME]
     ```
   - **Publish a Message**:
     ```bash
     gcloud pubsub topics publish [TOPIC_NAME] --message="[MESSAGE_CONTENT]"
     ```

2. **Cloud Run (Compute)**:
   - **Deploy a service**:
     ```bash
     gcloud run deploy [SERVICE_NAME] --image=[IMAGE_URL] --platform=managed
     ```
   - **List services**:
     ```bash
     gcloud run services list
     ```
   - **Get service URL**:
     ```bash
     gcloud run services describe [SERVICE_NAME] --format='value(status.url)'
     ```

3. **Workflows (AWS Step Functions equivalent)**:
    
    gcloud services enable workflows.googleapis.com
   - **Create a workflow**:
     ```bash
     gcloud workflows deploy [WORKFLOW_NAME] --source=[WORKFLOW_DEFINITION_FILE]
     ```
   - **Execute a workflow**:
     ```bash
     gcloud workflows execute [WORKFLOW_NAME] --data=[INPUT_DATA_FILE]
     ```
   - **List workflows**:
     ```bash
     gcloud workflows list
     ```

4. **Dataflow (AWS Kinesis Data Firehose equivalent)**:
   - **Create a Dataflow job**:
     ```bash
     gcloud dataflow jobs run [JOB_NAME] --gcs-location=[PIPELINE_SPECIFICATION_FILE] --region=[REGION]
     ```
   - **View job status**:
     ```bash
     gcloud dataflow jobs describe [JOB_NAME] --region=[REGION]
     ```
   - **Stop a job**:
     ```bash
     gcloud dataflow jobs cancel [JOB_NAME] --region=[REGION]
     ```

These commands allow you to use the corresponding services on Google Cloud Platform, providing the ability to create, manage, and operate these services. Use the appropriate commands based on your needs and scenarios.
    
## Exam Reference Information
The following are planning and deployment steps for processes related to these topics:

1. **Complete web application architecture with scalability and high availability**:

   - **Planning**:
     - Use a load balancer (such as HTTP load balancer) to distribute traffic across multiple instances.
     - Deploy instances across multiple regions or multiple zones within a region to improve availability.
     - Use auto-scaling to automatically adjust the number of instances based on load.
     - Use failover to protect the application from zone or regional failures.
     - Use health checks to monitor instance status and automatically replace failed instances.

   - **Deployment**:
     ```bash
     # Create load balancer
     gcloud compute forwarding-rules create [FORWARDING_RULE_NAME] \
         --load-balancing-scheme=INTERNAL \
         --backend-service=[BACKEND_SERVICE_NAME] \
         --region=[REGION] \
         --ports=80
     
     # Set up auto-scaling
     gcloud compute instance-groups managed set-autoscaling [INSTANCE_GROUP_NAME] \
         --max-num-replicas=[MAX_REPLICAS] \
         --min-num-replicas=[MIN_REPLICAS] \
         --target-cpu-utilization=[TARGET_CPU_UTILIZATION]
     
     # Set up failover
     gcloud compute addresses create [FAILOVER_IP_NAME] \
         --region=[REGION] \
         --addresses=[FAILOVER_IP]
     gcloud compute instance-groups managed set-named-ports [INSTANCE_GROUP_NAME] \
         --named-ports=[PORT_NAME]:[PORT_NUMBER]
     gcloud compute health-checks create http [HEALTH_CHECK_NAME] \
         --port=[PORT_NUMBER]
     gcloud compute backend-services add-backend [BACKEND_SERVICE_NAME] \
         --instance-group=[INSTANCE_GROUP_NAME] \
         --health-checks=[HEALTH_CHECK_NAME]
     gcloud compute target-pools create [TARGET_POOL_NAME] \
         --region=[REGION]
     gcloud compute target-pools add-instances [TARGET_POOL_NAME] \
         --instances=[INSTANCE_GROUP_NAME] \
         --instances-zone=[ZONE]
     gcloud compute forwarding-rules create [FAILOVER_RULE_NAME] \
         --region=[REGION] \
         --address=[FAILOVER_IP] \
         --target-pool=[TARGET_POOL_NAME]
     ```

2. **Resolve issues in existing architecture, build a highly available, scalable, secure, and resilient cloud deployment architecture**:

   - **Problem**: Single Point of Failure.
   - **Solution**: Deploy the same application across multiple regions or multiple zones within a region, and use a load balancer to distribute traffic.

3. **Handle continuous incoming requests**:

   - **Planning**: Use a load balancer and auto-scaling to handle large volumes of continuous incoming requests.
   - **Deployment**: Refer to the deployment steps for the complete web application architecture with scalability and high availability above.

4. **Provide a scalable three-tier web application architecture**:

   - **Problem**: Traditional three-tier architecture may not be able to handle increased traffic.
   - **Solution**: Use auto-scaling and load balancers to dynamically adjust resources at each tier to handle variable traffic volumes.

5. **Build cloud computing infrastructure for receiving, transforming, processing, and publishing information**:

   - **Planning**: Use Google Cloud Dataflow to process information streams.
   - **Deployment**:
     ```bash
     gcloud dataflow jobs run [JOB_NAME] \
         --gcs-location=[PIPELINE_SPECIFICATION_FILE] \


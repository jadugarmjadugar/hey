# ECS Anywhere

ECS Anywhere is an extension of Amazon ECS that will allow customers to deploy native Amazon ECS tasks in any environment. This will include the existing model on AWS managed infrastructure, as well as customer-managed infrastructure. All this without compromising on the value of leveraging a fully AWS managed, easy to use, control plane that’s running in the cloud, and always up to date.

Here are the supported platforms:

* Customer self managed infrastructure
* AWS Outposts
* AWS Wavelength
* AWS Local Zones
* AWS Regions

## Use-cases supported by ECS-Anywhere

ECS- Anywhere can solve the below use-cases:

* Manage legacy monolithic applications in customer data centers
* Run containers in the AWS Cloud and on-premises in a consistent manner
* Run applications on-premises for technical or compliance reasons
* Manage applications at edge locations consistently, efficiently, and reliably

## ECS-Anywhere Use-cases

* (Modernization) Customers moving to containers and migrating their workloads to AWS. Customers can now containerize their workloads on-premises first, make them portable, address on-premises dependencies, get familiar with AWS tools and get AWS-ready, followed by just updating the ECS services’ configuration from on-premises hardware to either Fargate or EC2.
* (Hybrid) Customers who need to run containerized workloads on both AWS and on-premises. Customers continue to run some workloads on-premises or other cloud environments for reasons such as data gravity, compliance, and latency requirements. Such customers need a single container orchestration platform for consistent tooling and deployment experience across all environments.
* (Hybrid) Customers who want to continue to utilize their on-premises infrastructure until their investments have fully amortized. Such customers are looking to use their on-premises infrastructure as base capacity while bursting into AWS during peaks or as their business grows. Over time, as they retire their on-premises hardware, they would continue to move the dial to use more compute on AWS until they have fully migrated.
* (IoT) Customers wanting to run container workloads at multiple edge locations. Such customers are looking to use ECS Anywhere to orchestrate containers at multiple edge locations. For example, these workloads could be gathering raw data from machines, or raw images from drones and processing them before sending to cloud.

----

## Getting started

* [Installation](Installation.md)
* [ECS Task](ecstasks.md)
* [ECS Service](ecsservice.md)
* [Integrate with SSM and Secrets manager](ssmsecrets.md)
* [Offload compute](offloadcompute.md)
* [CICD Pipeline for ECS-A](cicd.md)
* [Observability](observability.md)
* [Cleanup](cleanup.md)

----

## FAQ

1. **Which platforms and operating systems does ECS Anywhere support?**

    You can use ECS Anywhere with any VM (e.g. running on VMware, Microsoft Hyper-V, or OpenStack) or bare metal server running a supported Operating System (OS). The ECS Agent – software that allows a host to connect with the ECS control plane – is supported and tested for the LTS releases of: Amazon Linux 2, Bottlerocket, Ubuntu, RHEL, SUSE, Debian, CentOS and Fedora.
2. **Can I use ECS Anywhere with VMware Cloud on AWS (VMC)?**

    Yes, you can use ECS Anywhere with VMC. You can use the ECS-optimized Amazon Linux variants of VMware Virtual Machine Disk (VMDK) to launch instances. These ECS-optimized VMDKs are pre-configured with the latest version of the ECS agent, Docker daemon, and Docker runtime dependencies.
3. **How do I ensure the link between my on-premises compute and AWS cloud is secure?**

    The link between your on-premises compute and AWS cloud is secure by default and hence you do not need to take any additional actions. The ECS control plane running in the AWS region orchestrates containers by sending instructions to the ECS agent installed on each registered server over a secure link, which is authenticated using the instance IAM role credentials passed at the time of registering the server. Additionally, the ECS agent uses the AWS Systems Manager Agent to automatically and securely establish trust between the on-premises server and ECS control plane; its connection to AWS is encrypted with Transport Layer Security (TLS).
4. **What type of information flows from the on-premises compute back to the AWS region?**

    Only information necessary for managing the containers is sent to the ECS control plane running in the AWS region. As an example, information about host health, container activity (launched, stopped), and container health checks (if configured) may be sent back to the AWS region. This information enables AWS to provide alerting on health and capacity, and manage ECS tasks running on your on-premises compute. The contents of container memory, disk storage, or network traffic is not sent to the control plane.
5. **Can I have on-premises compute, EC2 instances, and Fargate in the same ECS cluster?**

    Yes, you can have on-premises compute, EC2 instances, and Fargate in the same cluster. This makes it easy for you to migrate your ECS workloads running on-premises to ECS in an AWS region on Fargate or EC2.
6. **Can I use the same ECS task definition for on-premises environments that I use to run ECS tasks on Fargate and/or EC2 instances?**

    Yes. An ECS task definition is a specification for a group of containers that must run co-located. ECS task definitions can be created so that they are compatible with on-premises compute, Fargate, and EC2, all in a single task definition.

7. **Can I use ECS Anywhere to run containers in air-gapped/disconnected environments?**

    No. ECS offers a cloud based and fully managed container orchestration solution that resides in an AWS region. Hence, it requires your on-premises compute to have a stable internet connection to communicate with the in-region ECS control plane.
8. **Which other ECS integrations with AWS services can I use when using ECS Anywhere?**

    With ECS Anywhere, you can get CloudWatch Metrics for your clusters and services, use the CloudWatch log driver to get your containers’ logs, as well as access the ECS CloudWatch Event stream to monitor your clusters’ events. You can use Task IAM Role and Task Execution Role to give your containerized applications fine-grained access control to AWS resources and use Cloud Map for service discovery. Additionally, if you are using Direct Connect or AWS VPN, you can use services such as Application Load Balancer (ALB) and Network Load Balancer (NLB) for load balancing, and PrivateLink if you do not wish to communicate with ECS’s public endpoint over an internet or Network Address Translation (NAT) gateway.
9. **Which third party solutions can I use when using ECS Anywhere?**

    ECS Anywhere works with the same tools that ECS in the cloud does, including Terraform, Consul, Datadog, Spinnaker, Jenkins, and many others.

10. **Some of the services that will not be supported part of ECS Anywhere GA?**

    Application load balancing, autoscaling, cloudmap service discovery and volume attachments (EBS & EFS) to ECS Tasks as these services are running on-prem.

----

## Resources

Here are some articles and documentations that you can refer to:

* [ECS Anywhere announcement blog](https://aws.amazon.com/blogs/containers/introducing-amazon-ecs-anywhere/)
* [Open source ECS Agent Gitrepo](https://github.com/aws/amazon-ecs-agent)

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.
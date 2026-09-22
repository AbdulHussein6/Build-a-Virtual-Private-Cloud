<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Virtual Private Cloud

**Project Link:** [View Project](https://nextwork.ai/projects/7f907ac7-2473-5c15-a8be-edb36581cdba)

**Author:** Abdul Hussein  
**Email:** abdulhussein@hotmail.se

---

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/7f907ac7-2473-5c15-a8be-edb36581cdba_2facf927)

## Introducing Today's Project!

In this project, I will demonstrate how to build a Virtual Private Cloud (VPC) in AWS, including configuring subnets, route tables, and gateways to control how resources communicate within and outside the network. I'm doing this project to learn the networking fundamentals that underpin most AWS services, since a solid understanding of VPCs is essential for designing secure, well-architected cloud environments — including how to separate public and private resources, control inbound and outbound traffic, and connect a VPC to the internet or other networks.

## Virtual Private Clouds (VPCs)

### What I did in this step

In this step, I created a Virtual Private Cloud (VPC), because a VPC is the foundational networking container for all my AWS resources.

### How VPCs work

VPCs (Virtual Private Clouds) are logically isolated sections of the AWS cloud where you can launch and manage resources within a private network that you define and control.

### Why there is a default VPC in AWS accounts

There was already a default VPC in my account ever since my AWS account was created. This is because would be able to launch resources (e.g. EC2 instances) and connect services together from Day 1 of using AWS. If it didn't exist, I would've had to learn how to create a VPC before you can use some of the services that need VPCs to function.

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/7f907ac7-2473-5c15-a8be-edb36581cdba_2facf927)

### Defining IPv4 CIDR blocks

CIDR (which stands for Classless Inter-Domain Routing) is a way to assign a whole block of IP addresses, kind of like creating a zone/area in a city.

## Subnets

### What I did in this step

In this step, I will created a subnet within my VPC, because a VPC on its own is just one large network range — subnets let me divide that range into smaller sections.

### Creating and configuring subnets

If your VPC is a city, subnets are like different neighborhoods inside your city. You use subnets to group resources with similar access rules and restrictions. Some subnets might be public areas that all resources can access (public subnets) while others are private areas with limited access (private subnets).

### Public vs private subnets

A public subnet is connected to the internet and a private subnet does not have direct internet access.

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/7f907ac7-2473-5c15-a8be-edb36581cdba_157c4219)

### Auto-assigning public IPv4 addresses

When I enabled auto-assign public IPv4 address for my subnet, any EC2 instance launched in that subnet will instantly get a public IP address so I won't have to create one manually.

## Internet gateways

### What I did in this step

In this step, I created an internet gateway, because a VPC and its subnets are private by default and have no way to communicate with the internet on their own. An internet gateway is the component that attaches to a VPC and allows traffic to flow between resources inside the VPC and the internet.

### Setting up internet gateways

An internet gateway connects your city (VPC) and the outside world (internet).

Attaching an internet gateway means resources in your VPC can now access the internet. The EC2 instances with public IP addresses also become accessible to users, so your applications hosted on those servers become public too.

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/7f907ac7-2473-5c15-a8be-edb36581cdba_4ae90410)

## Using the AWS CLI

### What I'm doing in this extension

In this project extension, I will use AWS CloudShell to run AWS CLI commands that create a VPC, subnet, and internet gateway, because doing this through the command line instead of the console teaches me how these resources can be created and managed programmatically.

### Exploring CloudShell and CLI

### Debugging my setup

To set up a VPC or a subnet, you can use the commands aws ec2 create-vpc and aws ec2 create-subnet. Make sure to avoid errors by including all required parameters — for a subnet, this means specifying both --vpc-id, to tell AWS which VPC the subnet belongs to, and --cidr-block, to define the subnet's own IP address range. I ran into a MissingParameters error because I left out --cidr-block, so the CLI didn't know what range of IP addresses to allocate. The fix was to add a CIDR block that falls within the VPC's range and uses a smaller subnet mask (e.g. /25 within a /24 VPC), since a subnet must be a subsection of its parent VPC rather than an equal or larger range.

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/7f907ac7-2473-5c15-a8be-edb36581cdba_9b2465411)

### Comparing CloudShell vs AWS Console

Compared to using the AWS Console, an advantage of using commands is speed and repeatability — once you know the right commands, you can create and configure resources like a VPC, subnet, and internet gateway in seconds, and the same commands can be saved and reused or scripted for automation. An advantage of using the Console is that it's much more visual and forgiving for troubleshooting — the resource map made it immediately obvious that my internet gateway wasn't attached and that my route table was missing a route to the internet, whereas with the CLI I had to actively query resources with commands like describe-internet-gateways to figure out what was wrong. Overall, I preferred using the Console for this project, since being able to see the relationships between my VPC, subnet, route table, and gateway visually made it much easier to understand what was actually happening — and to catch mistakes, like a missing CIDR block or an unattached gateway, faster than I could by reading 

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/7f907ac7-2473-5c15-a8be-edb36581cdba)*

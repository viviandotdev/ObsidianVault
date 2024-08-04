---
created: 2024-05-14 10:19 
modified: Tuesday 14th May 2024 10:19:02
alias: 
---
up::  [[How to build and deploy a sass]]
tags:: #aws #deploy #backend #api 
type:: #note/how-to
links::
## How to deploy backend using AWS EC2 

**Launch a EC2 instance**
1. Go to [Instances](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#Instances:)
2. Select **Launch Instance**
3. Name the instance (ex. twitter-server)
4. Under **Application and OS images**
	Select **ubuntu**
5. Under **Instance type**
	Select **t2.medium**
6. Under **key-pair(login)**
	create key pair and install pem file
7. Under **Network Settings**
	![[Screenshot 2024-05-14 at 6.16.14 PM.png]]
**Create an IP address for your machine**
1. Go to [Elastic IPs](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#Addresses:)
2. Select **Allocate Elastic IP address**
3. Select **Allocate**
4. Go back to  [Elastic IPs](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#Addresses:)
	select Actions -> Associate Elastic IP Address
	select the instance to associate your ip address to

**Update instance a security group to allow port 8000**
1. Select your instance and to the security tab
2. Select the security group attached to the instance
	![[Screenshot 2024-05-14 at 6.09.18 PM.png]]
3. Select edit inbound rules and add 2 inbound rules for port 8000 
	![[Screenshot 2024-05-14 at 6.11.13 PM.png]]
 **SSH into the EC2 instance and launch api**
1. clone the repo
2. set up and install node on the instances
	[How to install Node.js 20 on Ubuntu 20.04 LTS - Josh Sherman](https://joshtronic.com/2023/04/23/how-to-install-nodejs-20-on-ubuntu-2004-lts/)
```
sudo apt update
sudo apt upgrade
sudo apt install -y curl
```
```
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
node --version
```
3. update the .env file
4.  install pnpm
```
curl -fsSL https://get.pnpm.io/install.sh | sh -
```
5. install dependences
```
pnpm i
```
6. update database url and generate and then migrate the database
```
pnpm db:generate
pnpm db:migrate:dev
```
7. run build command to create the build
```
pnpm 
```
9. Install process manager pm2
```
sudo npm install pm2 -g
```
10. Go into the build folder and run the build
```
pm2 start index.js
```

**Visit the public IP address at port 8000 to view your deployed backed**
```
52.5.127.220:8000/graphql
```


### How to load balance between instances
**Create a application load balancer**
1. Go to [Load balancers](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#LoadBalancers:)
2. Select **Create Load Balancer**
	- Create application load balancer
	- Name your load balancer (app-name-alb)
	- Under **Network Mappings**
		- select all availability zones
	- Under **Security Groups**
		- select the security group created for this API

**Create a target group** (load balancer routes requests to targets in the target group)
1. Go to [Target Groups](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#TargetGroups:)
2. Select **Create Target Groups**
3. Name your target group
4. Select the instances for your target group
	- Set the Port for selected instances to 8000 
	- Select **include as pending below**
	- Review your targets and then create target group
	![[Screenshot 2024-05-14 at 5.59.02 PM.png]]

### Add Cloudfront CDN

1. Go to [Cloudfront Distributions](https://us-east-1.console.aws.amazon.com/cloudfront/v4/home?region=us-east-1#/distributions)
2. Select **Create distribution**
3. Under **Origin**
	1. Select the Elastic load Balancer created as the origin domain
	2. Select HTTP only protocol
4. Under **View**
	![[Screenshot 2024-05-14 at 6.34.01 PM.png]]
5. Under **Cache key and origin requests**
	1. Create cache policy 
		Under **Cache key settings** 
		Headers -> Include the following headers
		![[Screenshot 2024-05-14 at 6.35.56 PM.png]]
	1. Create Cache Policy
6. Select the custom cache policy
7. Select **Create Distribution**


**DevOps Flow**
1. Automate builds
2. Automate deployments p
**Sources**
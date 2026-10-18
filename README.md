# Project-4
This is my 4 project.
AWS Blue-Green Deployment Using Application Load Balancer (ALB)

📌 Project Overview

This project demonstrates the implementation of a Blue-Green Deployment strategy using AWS Application Load Balancer (ALB). The main objective is to deploy a new application version while keeping the existing version available and allowing traffic to be switched between them.

The project uses two Amazon EC2 instances, two Target Groups, and one Application Load Balancer. The Blue environment hosts Version 1 of the application, while the Green environment hosts Version 2.

Traffic is switched between the two environments by updating the default action of the ALB HTTP listener. If an issue occurs in the Green environment, traffic can be switched back to the Blue environment for rollback.

🎯 Project Objectives

- Implement Blue-Green Deployment on AWS.
- Configure an Application Load Balancer.
- Create and configure two Target Groups.
- Deploy two application versions on separate EC2 instances.
- Configure HTTP listener forwarding.
- Perform deployment switching and rollback.
- Monitor target health using health checks.
- Understand traffic management and high availability concepts.

🏗️ Architecture Structure


<img width="1376" height="768" alt="image_d4dd7a57" src="https://github.com/user-attachments/assets/9e829ab7-669d-4d7a-ae0c-9107c98beb89" />

                    
      

        Traffic Switch: Blue <--> Green
        Rollback: Green --> Blue

Note: The listener forwards traffic to the Target Group selected as its default action. The diagram shows the two available environments, not simultaneous traffic forwarding.

☁️ AWS Services Used

AWS Service| Purpose
Amazon EC2| Hosts the application versions
Application Load Balancer| Receives HTTP requests and forwards traffic
Target Groups| Register and monitor the EC2 targets
ALB Listener| Controls traffic forwarding
Security Groups| Control inbound and outbound traffic
Amazon VPC| Provides network connectivity

🖥️ Environment Configuration

Blue Environment

- EC2 Instance: "blue-server"
- Target Group: "blue-tg"
- Application Version: Version 1
- Sample webpage: "BLUE - Version 1"

Green Environment

- EC2 Instance: "green-server"
- Target Group: "green-tg"
- Application Version: Version 2
- Sample webpage: "GREEN - Version 2"

Load Balancer

- Name: "blue-green-alb"
- Type: Application Load Balancer
- Listener: HTTP port 80
- Default action: Forward to the selected Target Group
- Scheme: Internet-facing

⚙️ Implementation Steps

1. Create two EC2 instances in the same VPC.
2. Install and configure Nginx on both instances.
3. Deploy Version 1 on the Blue instance and Version 2 on the Green instance.
4. Create "blue-tg" and register the Blue instance.
5. Create "green-tg" and register the Green instance.
6. Configure HTTP health checks and verify that both targets become healthy.
7. Create an Application Load Balancer across suitable subnets in different Availability Zones.
8. Configure the HTTP:80 listener with "blue-tg" as the initial default action.
9. Open the ALB DNS name in a browser and verify Version 1.
10. Change the listener's default action from "blue-tg" to "green-tg".
11. Refresh the same ALB DNS URL and verify Version 2.
12. Switch back to "blue-tg" to demonstrate rollback.

🔄 Blue-Green Deployment Workflow

Phase 1: Blue is Live

The ALB forwards incoming requests to "blue-tg", which directs traffic to the Blue EC2 instance running Version 1.

Phase 2: Green is Prepared

Version 2 is deployed to the Green EC2 instance. Its Target Group health is checked before switching production traffic.

Phase 3: Traffic Switching

The ALB listener's default action is updated from "blue-tg" to "green-tg". New requests are directed to Version 2.

Phase 4: Rollback

If Version 2 has a problem, the listener's default action is switched back to "blue-tg", restoring traffic to Version 1.

🧪 Testing and Validation

- Verify that both EC2 instances are running.
- Confirm that both Target Groups report healthy targets.
- Access the ALB DNS name and verify the Blue application version.
- Change the default listener action and verify the Green application version.
- Switch back to Blue and verify rollback.
- Check the application response and target health after each change.

🔐 Security Configuration

- Allow HTTP port 80 on the ALB Security Group for intended users.
- Allow HTTP port 80 on the EC2 Security Group from the ALB Security Group.
- Restrict SSH access to a trusted IP address.
- Use appropriate subnet routing and network access controls.

💡 Key Learnings

- Application Load Balancer configuration
- Target Group registration and health checks
- EC2 and Nginx deployment
- Blue-Green Deployment strategy
- Listener-based traffic switching
- Rollback and release management
- AWS networking and Security Groups

📈 Benefits

- Simplifies switching between application versions.
- Supports rollback to the previous version.
- Allows the new version to be prepared and checked before traffic switching.
- Helps reduce deployment-related downtime when configured correctly.
- Provides practical experience with AWS load balancing and deployment strategies.

⚠️ Important Notes

- This project uses manual traffic switching; it does not implement an automated CI/CD pipeline.
- No Auto Scaling Group is used.
- Both environments should be tested before production traffic is switched.
- Blue-Green deployment does not guarantee zero downtime in every situation.
- AWS resources such as EC2 instances and the Application Load Balancer may incur charges. Delete resources when the lab is complete.

🏁 Conclusion

This project demonstrates how to implement a basic Blue-Green Deployment strategy using AWS Application Load Balancer, EC2 instances, and Target Groups. It provides hands-on experience in application deployment, traffic switching, health monitoring, and rollback.

The project is suitable for AWS Cloud and DevOps learning, practical demonstrations, and a technical portfolio.

Technologies: AWS EC2 | Application Load Balancer | Target Groups | Nginx | VPC | Security Groups

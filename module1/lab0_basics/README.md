# SEIR Foundations - Module 1, Lab 0: EC2 Basics

## Evidence

| Deployment | Instance ID | Public IPv4 | Connection method | Screenshot | Terminated? |
|---|---|---|---|---|---|
| 1 | i-09852d8b02015310b | 52.87.185.194 | EC2 Instance Connect | screenshots/deployment-1.png | Yes |
| 2 | i-0daefc760f08aa6c6 | 32.192.7.27 | EC2 Instance Connect | screenshots/deployment-2.png | Yes |
| 3 | i-0566d92f0d87edf9c | 54.197.187.200 | EC2 Instance Connect | screenshots/deployment-3.png | Yes |

Terminated instances: screenshots/Shibumi_Terminated_deployments.png

## What I did

**Deployment 1:** I launched an Amazon Linux 2023 t3.micro instance in us-east-1 with the provided User Data script, waited for the status checks to pass, and connected with EC2 Instance Connect. The SEIR dashboard appeared on login.

**Deployment 2:** I launched a new instance from my saved launch template, connected with EC2 Instance Connect, and the dashboard displayed as before.

**Deployment 3:** I repeated the launch from the template, connected, and captured the dashboard.

## What the dashboard showed

On deployment 1, CPU was about 0% busy on 2 vCPUs, and memory use was about 179 MB of 913 MB. About 21% of the 8 GB root disk was used, and uptime was 13 minutes. These numbers show a small, idle server: the User Data script had finished, and nothing heavy was running.

## What got easier

Launching from the saved template was faster than configuring everything by hand, because the AMI, instance type, key pair, security group and User Data were all preset.

## Problems and fixes

- Cloning the class repo failed on Windows because of an invalid file path (`module1/lesson1_ec2/iam/PERMISSIONS.md`), so I worked in the browser instead.
- "Create template from instance" was greyed out until I selected the instance first.

## Cleanup

I kept the launch template (`Shibumi_seir-lab0-template`) and terminated all three practice instances.

***YES - I had CLAUDE write up what I did.***

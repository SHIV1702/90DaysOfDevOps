# Day 08 - Cloud Deployment with Nginx

## Objective

Deploy a web server on a cloud instance, configure security groups, access it through the internet, and collect logs.

## Commands Used

ssh -i day08.pem ubuntu@<PUBLIC-IP>

sudo apt update
sudo apt upgrade -y

sudo apt install nginx -y

sudo systemctl status nginx
sudo systemctl enable nginx

curl localhost

sudo tail -20 /var/log/nginx/access.log
sudo tail -20 /var/log/nginx/error.log

cat /var/log/nginx/access.log > ~/nginx-logs.txt

scp -i day08.pem ubuntu@<PUBLIC-IP>:~/nginx-logs.txt .


## Challenges Faced

1. HTTP page was not accessible initially.
2. Security Group did not allow inbound traffic on port 80.
3. Added HTTP rule and verified Nginx service status.
4. Web page became accessible successfully.

## What I Learned

* How to launch an EC2 instance.
* How to connect remotely using SSH.
* How to install and manage Nginx.
* How security groups control network access.
* How to view and extract Nginx logs.

## Why This Matters for DevOps

* Cloud server provisioning is a daily DevOps task.
* SSH is essential for remote server administration.
* Web server deployment is a fundamental production activity.
* Log analysis helps troubleshoot issues.
* Security groups are the first layer of network security.

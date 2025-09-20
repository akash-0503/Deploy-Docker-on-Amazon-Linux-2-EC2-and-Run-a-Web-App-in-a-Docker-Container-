Step1.
First we should have the AWS account created or with IAM User you can login
=
<img width="1920" height="949" alt="Screenshot (11)" src="https://github.com/user-attachments/assets/dfe93707-7e5e-41b6-ab3d-b2fb8dc86903" />

Step 2: Launch EC2 Instance 
=
1. Go to AWS Management Console → EC2 → Launch Instance. 
2. Enter name: webapp
3. Choose AMI: Amazon Linux 2 (64-bit x86). 
4. Select Instance Type: t2.micro (Free Tier eligible). 
5. Key Pair: Choose or create a new .pem key. 
6. Security Group: Allow SSH (22) and HTTP (80). 
7. Launch the instance and copy the Public IPv4 Address. 
<img width="1864" height="874" alt="Screenshot 2025-09-21 002912" src="https://github.com/user-attachments/assets/43466e5d-a394-4852-a8d3-dc6ced32fbad" />
<img width="1892" height="842" alt="Screenshot 2025-09-21 002958" src="https://github.com/user-attachments/assets/eb23d108-d0cc-47d7-80ac-22f780cf16bf" />
<img width="1880" height="848" alt="Screenshot 2025-09-21 003023" src="https://github.com/user-attachments/assets/d7287be1-0dbf-453a-8117-8c34b141a5ba" />
<img width="1898" height="363" alt="Screenshot 2025-09-21 014941" src="https://github.com/user-attachments/assets/b57edad3-963c-457b-b7c8-001730bfd13b" />

Step 3: Connect to EC2 via SSH 
=

From your terminal: 

ssh -i your-key.pem ec2-user@<EC2-Public-IP> 

<img width="1885" height="861" alt="Screenshot 2025-09-21 003211" src="https://github.com/user-attachments/assets/938a0628-3cc3-4cb5-9903-8503e39f9cfd" />

Step 4: Install Docker on Amazon Linux 2 
=
Update and upgrade system: 

sudo yum update -y 

sudo yum upgrade -y 

Install utilities: 

sudo yum install -y yum-utils 

Enable and install Docker: 

sudo amazon-linux-extras enable docker 

sudo yum install -y docker 

Check Docker version: 

docker --version 

Start and enable Docker: 

sudo service docker start 

sudo systemctl enable docker 

sudo systemctl status docker 

(Optional) Add ec2-user to Docker group: 

sudo usermod -aG docker ec2-user 

exit

It is the docker installation

Then

Reconnect via SSH: 

ssh -i your-key.pem ec2-user@<EC2-Public-IP> 

groups 

Step 5: Run Apache in Docker 
=

Pull Apache image: 

sudo docker pull httpd:latest 

Run Apache container on port 80: 

sudo docker run -d -p 80:80 --name my-apache-app httpd:latest 

List containers: 

sudo docker container ls -a 

Start container (if stopped): 

sudo docker container start my-apache-app 
<img width="1896" height="791" alt="Screenshot 2025-09-21 010046" src="https://github.com/user-attachments/assets/7d6cb074-1bf6-487b-a999-df79527fa604" />

Step 6: Customize the Web Page 
=
Enter container shell: 

sudo docker exec -it my-apache-app /bin/bash 

Navigate to Apache web root: 

cd /usr/local/apache2/htdocs 

Create a custom index.html: 

echo "MyWebsite - Running on Apache inside Docker" > index.html cat index.html 

ls

cat index.html 

Exit container: 

exit
<img width="1897" height="849" alt="Screenshot 2025-09-21 010112" src="https://github.com/user-attachments/assets/9f9d9bae-0347-4183-b20e-d0af7a056f4f" />

Step 7: Test the Web App 
=
From your local machine: 

curl http://<EC2-Public-IP> 

Or open in browser: 

http://<EC2-Public-IP> 

You should see: 

MyWebsite - Running on Apache inside Docker 
<img width="1612" height="310" alt="Screenshot 2025-09-21 010939" src="https://github.com/user-attachments/assets/6bdaa96f-4e33-47cb-b516-a4949a0af0b3" />

Step 8: Manage and Monitor 
=
Inspect container: 

sudo docker container inspect my-apache-app 

Check performance: 

sudo docker container stats my-apache-app 
<img width="1892" height="698" alt="Screenshot 2025-09-21 010430" src="https://github.com/user-attachments/assets/5a2c20cb-cd5f-4a70-9915-81a117bd1047" />
<img width="1889" height="748" alt="Screenshot 2025-09-21 010508" src="https://github.com/user-attachments/assets/fa206f28-1f79-4c72-9be7-cd29329a714f" />
<img width="1855" height="294" alt="Screenshot 2025-09-21 011210" src="https://github.com/user-attachments/assets/188ca383-443f-427b-a91f-6c7a47c982eb" />
Lab Completed✅               

You now have an Amazon Linux 2 EC2 instance with Docker installed, running an Apache 

container that serves a custom webpage. 

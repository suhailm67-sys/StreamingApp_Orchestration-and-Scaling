# Graded Project on Orchestration and Scaling
Graded Project on Orchestration and Scaling on Streaming App

## Project Workflow

### Step 1: Version Control with Git
1. Fork the main repository into your GitHub account.
  - Open the repo link - `https://github.com/UnpredictablePrashant/StreamingApp.git`
  - Click on `fork`
  - The main repo is now forked to the Git Hub account - <img width="1577" height="581" alt="image" src="https://github.com/user-attachments/assets/b196db13-bae8-4c98-8e4e-7554293d843a" />

2. Clone the fork on the local machine - `git clone https://github.com/suhailm67-sys/StreamingApp_Orchestration-and-Scaling.git` - <img width="1442" height="211" alt="image" src="https://github.com/user-attachments/assets/c4f645ff-5129-4c78-8056-88d1110b55ff" />
3. Verify remote - `git remote -v` - <img width="1372" height="76" alt="image" src="https://github.com/user-attachments/assets/5c9e8495-07c2-4837-872d-5ec1155f3d3f" />
4. Add Upstream Repository - `git remote add upstream https://github.com/UnpredictablePrashant/StreamingApp.git` - <img width="1452" height="160" alt="image" src="https://github.com/user-attachments/assets/1564a929-4e0d-44d7-bbfc-fae056b96bd4" />
5. Sync with Upstream
  - Whenever the original repository changes, fetch latest - `git fetch upstream` - <img width="1432" height="206" alt="image" src="https://github.com/user-attachments/assets/9720609d-ba00-4cbc-a038-136fead637da" />
  - Switch - `git checkout main` - <img width="1436" height="71" alt="image" src="https://github.com/user-attachments/assets/5ad4f8b1-c471-43f6-bd07-c27564f5298d" />
  - Merge - `git merge upstream/main` - <img width="1497" height="52" alt="image" src="https://github.com/user-attachments/assets/270c16ba-9706-49a4-953e-771b8f71e326" />
  - Push to your GitHub - `git push origin main` - <img width="1452" height="67" alt="image" src="https://github.com/user-attachments/assets/5453913d-bae4-41ec-ad99-0078f96c0012" />

### Step 2: Prepare the MERN Application
Since docker file has already been setup and configured, not required to setup the docker file again. 
Docker files are available in backend >> adminService | authService | chatService | streaming | Service >> Dockerfile, frontend >> Dockerfile

### Step 3: Download, Install and configure AWS CLI
```# Download and install AWS CLI v2
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
./aws/install

# Verify
/usr/local/bin/aws --version
# aws-cli/2.35.11
```
```
aws configure
# AWS Access Key ID: [your-access-key]
# AWS Secret Access Key: [your-secret-key]
# Default region: us-east-1
# Default output: json

# Verify
aws sts get-caller-identity
```
<img width="1577" height="150" alt="image" src="https://github.com/user-attachments/assets/1daf3759-be2c-4d5c-b20c-74888196bb76" />

### Step 4: Creating ECR Repositories 
Create repository for each services seperately
1. Frontend Service - `aws ecr create-repository --repository-name frontend --region us-east-1` - <img width="1517" height="421" alt="image" src="https://github.com/user-attachments/assets/94319ab8-e7b9-4ae1-aae3-cfec4f9fc440" />
2. Auth Service - `aws ecr create-repository --repository-name auth-service --region us-east-1` - <img width="1507" height="426" alt="image" src="https://github.com/user-attachments/assets/e57e213f-9b81-433a-aed4-bd3bb10baeb7" />
3. Streaming Service - `ws ecr create-repository --repository-name streaming-service --region us-east-1` - <img width="1506" height="426" alt="image" src="https://github.com/user-attachments/assets/1939136b-f993-4b7f-822a-277b16b0ad54" />
4. Admin Service - `aws ecr create-repository --repository-name admin-service --region us-east-1` - <img width="1522" height="437" alt="image" src="https://github.com/user-attachments/assets/ee4106af-5160-4a12-a9eb-89ef6cb664de" />
5. Chat Service - `aws ecr create-repository --repository-name chat-service --region us-east-1` - <img width="1520" height="425" alt="image" src="https://github.com/user-attachments/assets/52d64366-d383-4a45-b589-e2ba13878024" />

### Step 5: Build, Tag and Push Docker Images
#### 1. Frontend Service
  1. Build the image - `docker build -t frontend:latest ./frontend` - <img width="1721" height="941" alt="image" src="https://github.com/user-attachments/assets/581a02c1-6e80-4731-ba7d-bb2a6bd03132" />
  2. Tag the image - `docker tag frontend:latest 663130434850.dkr.ecr.us-east-1.amazonaws.com/frontend:latest` - <img width="1882" height="66" alt="image" src="https://github.com/user-attachments/assets/1f002338-05d6-4d6b-8d2b-9cc93d0984d0" />
  3. Push the image - `docker push 663130434850.dkr.ecr.us-east-1.amazonaws.com/frontend:latest` - <img width="1192" height="325" alt="image" src="https://github.com/user-attachments/assets/6baca303-cf05-47d9-a74d-97fd4be8a7ff" />
#### 2. Follow the above same process to Build, Tag and Push the remaining Auth, Streaming, Admin and Chat service images
#### 3. Verify the Images in ECR
1. From AWS Console - `AWS Console >> Amazon ECR >> Private repositories` - <img width="1907" height="587" alt="image" src="https://github.com/user-attachments/assets/bda202db-842a-4a2f-932d-418ef3c5f3e4" />
2. From Power Shell - `aws ecr list-images --repository-name frontend --region us-east-1` - <img width="1865" height="382" alt="image" src="https://github.com/user-attachments/assets/018231a6-6e92-4b3f-80a2-b371b662c93c" />
#### Similarly verify from the remaining services (Admin, Auth, Chat and Streaming)

### Step 6: Continuous Integration (CI) using Jenkins
#### Set Up Jenkins
1. Access Jenkins from the URL- https://jenkinsacademics.herovired.com/
2. Add AWS Credentials to Jenkins
  1. Go to Manage Jenkins >> Credentials
  2. Click Add Credentials and select AWS Credentials
  3. Update the AWS Access Key and AWS Secret Key, then click on Create - <img width="680" height="111" alt="image" src="https://github.com/user-attachments/assets/3f59985f-b2f9-4d7e-8c18-058e9316b9a5" />

####  Create Jenkins Pipeline Job
1. New Item Name: Suhail-StreamingApp-Pipeline
2. Select Pipeline OK
3. Pipeline section:
  1. Definition: Pipeline script from SCM
  2. SCM: Git
  3. Repository URL: https://github.com/suhailm67-sys/StreamingApp_Orchestration-and-Scaling.git
  4. Branch: */main
  5. Script Path: Jenkinsfile and Save
<img width="1012" height="692" alt="image" src="https://github.com/user-attachments/assets/5ed08b39-3207-406c-8090-baf3482a3f84" />

### Step 7: Install Jenkins on an AWS EC2 instance
1. Create a EC2 instance first to launch Jenkins in it - <img width="1620" height="222" alt="image" src="https://github.com/user-attachments/assets/2c9582dc-536e-430d-9583-1664b5152b9c" />
2. SSH into the EC2 instance and install the prequisits like `sudo apt update`,`sudo apt upgrade -y`, `sudo apt install openjdk-21-jdk -y`, `sudo apt install git -y`
3. Install and start docker in EC2 - `sudo apt install docker.io -y`, `sudo systemctl start docker`, `sudo systemctl enable docker` - <img width="1121" height="355" alt="image" src="https://github.com/user-attachments/assets/4887b90e-bc64-4afe-a0b3-5f8ef80f898d" />
4. Install AWS CLI in EC2 - `sudo apt install unzip curl -y`, `curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"`, `unzip awscliv2.zip`, `sudo ./aws/install`
5. Install kubectl v1.29 (EKS compatible) - `curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.29.6/2024-07-12/bin/linux/amd64/kubectl`, `chmod +x kubectl`, `mv kubectl /usr/local/bin/kubectl`
6. Install eksctl - `curl --silent --location "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_Linux_amd64.tar.gz" | tar xz -C /tmp`, `mv /tmp/eksctl /usr/local/bin`
7. Install Helm - `curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash`
8. Verify all - `kubectl version --client`, `eksctl version`, `helm version` - <img width="1457" height="182" alt="image" src="https://github.com/user-attachments/assets/af10e583-7715-4547-8fb3-6b9f3c89c076" />
9. Install Jenkins - `curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key \ | sudo tee \ /usr/share/keyrings/jenkins-keyring.asc > /dev/null`, `echo deb \
[signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/ \
| sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null`, `sudo apt update`, `sudo apt install jenkins -y`
10. Configure necessary plugins and credentials - `sudo systemctl enable jenkins`, `sudo systemctl start jenkins` and install plugins by logging in to the EC2 `http://EC2-IP:8080` - <img width="1912" height="592" alt="image" src="https://github.com/user-attachments/assets/ae0b894f-ee05-4a47-8bab-e8b7b3b8250f" />


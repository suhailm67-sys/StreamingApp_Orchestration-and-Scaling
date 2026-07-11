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
  3. Update the AWS Access Key and AWS Secret Key, then click on Create
#### 

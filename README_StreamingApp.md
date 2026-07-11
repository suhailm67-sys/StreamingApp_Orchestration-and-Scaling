# Graded Project on Orchestration and Scaling
Graded Project on Orchestration and Scaling in Jenkins

## Project Workflow

### Step 1: Version Control with Git
1. Fork the main repository into your GitHub account.
  - Open the repo link - `https://github.com/UnpredictablePrashant/StreamingApp.git`
  - Click on `fork`
  - The main repo is now forked to the Git Hub account - <img width="1577" height="581" alt="image" src="https://github.com/user-attachments/assets/b196db13-bae8-4c98-8e4e-7554293d843a" />

2. Clone the fork on the local machine - `git clone https://github.com/suhailm67-sys/StreamingApp_Orchestration-and-Scaling.git` - <img width="1442" height="211" alt="image" src="https://github.com/user-attachments/assets/c4f645ff-5129-4c78-8056-88d1110b55ff" />
3. Verify remote - `git remote -v` - <img width="1372" height="76" alt="image" src="https://github.com/user-attachments/assets/5c9e8495-07c2-4837-872d-5ec1155f3d3f" />
4. Add Upstream Repository - `git remote add upstream https://github.com/UnpredictablePrashant/StreamingApp.git` - <img width="1887" height="156" alt="image" src="https://github.com/user-attachments/assets/c826f6b6-e245-44c3-9bcd-27d73b263ec6" />
5. Sync with Upstream
  - Whenever the original repository changes, fetch latest - `git fetch upstream` - <img width="1576" height="235" alt="image" src="https://github.com/user-attachments/assets/a8916091-d45b-4f05-a829-056a7e5fbc4d" />
  - Switch - `git checkout main` - <img width="1533" height="65" alt="image" src="https://github.com/user-attachments/assets/ed298edf-7022-4eea-8206-ff8ed0e526c0" />
  - Merge - `git merge upstream/main` - <img width="1612" height="47" alt="image" src="https://github.com/user-attachments/assets/fe5b383a-be74-4e94-94b8-9b9b69efd496" />
  - Push to your GitHub - `git push origin main` - <img width="1627" height="77" alt="image" src="https://github.com/user-attachments/assets/ef159e89-fae6-4278-abc5-d4a32c5d1c91" />

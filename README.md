# X-HEC MLOps Class Introductory Workshop


1. Form groups of 3 to 4 persons, ideally with complementary skills (data, math, SE,...)
   - Fill group file

2. Access your AWS machine via VS Code

   - Download VS Code
   - Open « Remote Explorer »
   - Ask for your machine's Public IPv4 URL & your key set 
   - Add SSH connection (ou  can test you ssh command in your terminal to see if there are any errors)

```
sudo  chmod 400 x-hec-key-pair.pem
ssh-add x-hec-key-pair.pem
ssh -v -i x-hec-key-pair.pem ec2-user@{url-name}
```

3. Fork & star this repository

   - Create a git account, star the repository
   - Create a folder with your group name
  
```
mkdir {group_name}
cd {group_name}
git clone (fork?) ...
cd [REPO NAME]
```

4. Create a Python Django App

- Create a conda environment

```
conda create -n {group_name} python=3.8
conda activate {group_name}
```

- Create a django app 

- Deploy locally your django App

- Create your first API Call :  Call on /health/ that returns healthy 200

1. Create a view
2. Configure your URLs
3. Check Local Host


5. Create an API Call with a Gen AI Component : Answering questions with HuggingFace's Inference Points.

- Create a new view (GET) and url access
- Ask for the API Key and URL
- Add a call to HF Generate
- Debug & deploy

 














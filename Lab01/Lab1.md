# Lab 01 - Simulate a Repository Migration from Azure DevOps to GitHub Enterprise Cloud using GitHub CLI and GEI

In this lab, you will learn how to **simulate and validate the
migration** of a source code repository from **Azure DevOps (ADO)** to
**GitHub Enterprise Cloud (GEC)** using the **GitHub CLI**, the **GitHub
Enterprise Importer (GEI)**, and the **ado2gh CLI extension**.  
This involves both a **dry-run** and a **real migration**, using PATs
and validated permissions to confirm readiness and ensure smooth
migration of project assets.

**Objective**:

To simulate and validate a successful migration from **Azure DevOps** to
**GitHub Enterprise Cloud** using **GitHub CLI**, **GEI**, and the
**ado2gh extension**, and ensure project readiness for production
migration.

**Pre-requisites**

Ensure the following before you start:

- A GitHub account with repo creation access
    
- Azure DevOps project and repo access

- GitHub CLI installed +++https://cli.github.com+++

- GitHub Enterprise Importer CLI (gh-gei) installed

- Two Personal Access Tokens (PATs):

  - **GitHub PAT** (with repo, admin:org, workflow scopes)

  - **Azure DevOps PAT** (with Code (read) and Project & Team scopes)

### Task 1: Start GitHub Enterprise Cloud Free Trial

1.  Open a browser and go to +++https://github.com/enterprise/trial+++ and
    click on sign in. sign in with your GitHub account.

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image1.png)

2. Open a new tab and go to +++https://github.com/enterprise/trial+++. Click on **Start your free trial.**

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image2.png)

3.  Click on **Get started with personal accounts.**

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image3.png)

4.  Enter below values and then click on **Create enterprise.**

    1.  Enterprise name : +++tfdevops-migr@lab.LabInstance.Id+++ (This must be a unique value)

    2.  Industry : education (you can select as per your requirement)

    4.  Number of employees :0-50

    5.  Enter Contact information : Your user name as Admin name and your GitHub account email id as Admin work email

    6.  Verify account

    7.  Accept trial term

    ![A screenshot of a computer AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image4.png)

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image5.png)

5.  Click on **Skip for now** button to sip the payment method.

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image6.png)

6.  Enter **Organization account name :** +++devopstogtihub@lab.LabInstance.Id+++ and click on **Create organization and continue** button.

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image7.png)

    ![A screenshot of a computer AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image8.png)

7. Click on **People** tab to check the license 

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image9.png)

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image10.png)

### Task 2: Install and Authenticate GitHub CLI

1.  From Start menu, search for +++Powershell+++ and run Powershell as **administrator**.

    ```winget install --id GitHub.cli```

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image11.png)

    ![A computer screen with white text and blue text AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image12.png)

2.  Close the PowerShell window.

3.  By default, GitHub CLI is installed in below location. Add GitHub
    CLI to system PATH

    +++C:\Program Files\GitHub CLI+++

4.  in Start menu search for +++Environment Variables+++ and select **Edit the system environment variables**

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image13.png)

5.  In the **System Properties** window, click **Environment
    Variables**.

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image14.png)

6.  Under **System variables**, find and select **Path**, then
    click **Edit**.

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image15.png)

7.  Click **New** and **add** GitHub CLI path and then click 
    **OK -\> OK -\>OK**.

    +++C:\Program Files\GitHub CLI+++

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image16.png)

8.  Restart the PowerShell and run below command login.

    +++gh --version+++

    +++gh auth login+++

    ![A computer screen with white text AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image17.png)

9.  Follow the interactive prompts:

    1.  Choose **GitHub.com**
    2.  Select **HTTPS**
    3.  Authenticate git wiht your GitHub credentials :Yes
    4.  Login with a browser
    5.  Copy the generated code and press enter to device login in a browser
    6.  Sign in with your GitHub credntials.
       

    ![A screen shot of a computer AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image18.png)

    ![A computer screen shot of a black screen AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image19.png)

10. Enter the copied code and then click on **Continue** button

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image20.png)

10. Click on **Authorize github** button.

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image21.png)

    ![A screenshot of a computer AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image22.png)

11. Switch back to PowerShell window.

    ![A computer screen shot of a computer program AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image23.png)

12. After login, confirm by running:

    +++gh auth status+++

    ![A screenshot of a computer program AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image24.png)

13. Verify GEC Org Admin Permissions. If you can list org repos, you're properly authenticated and ready.Replace ORG-NAME with your organization name and then run it. ( eg: GitHub organization name is +++devopstogtihub@lab.LabInstance.Id+++ and must be a unique value)

    +++gh repo list ORG-NAME+++

    ![A screen shot of a computer AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image25.png)

### Task 3: Install the GEI (GitHub Enterprise Importer) Extension

1.  Run below command to install GitHub Enterprise importer extension.

    +++gh extension install github/gh-gei+++

    ![A screen shot of a computer AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image26.png)

2.  Run below command to verify installation:

    +++gh gei -h+++

    ![A screen shot of a computer AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image27.png)


### Task 4: Create an Azure DevOps personal access token

1.  Create an Azure DevOps personal access token (PAT). Open a new tab in your browser and navigate to +++https://portal.azure.com+++ and sign in with your cloud slice account.

    - Username: +++@lab.CloudPortalCredential(User1).Username+++  
   
    - Temporary Access Pass (TAP): +++@lab.CloudPortalCredential(User1).AccessToken+++

2. Cancel "Welcome to Microsoft Azure" window
   
3. Enter  +++Azure DevOps+++ in the search bar and select **Azure DevOps organizations**.

    ![A screenshot of a computer AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image29.png)

3.  Click on **My Azure DevOps Organizations** hyper link.

    ![A screenshot of a computer AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image30.png)

4.  Click on **Create new organization** button.

    ![A screenshot of a computer AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image31.png)

5.  Click on **Continue**.

    ![A screenshot of a computer error AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image32.png)

6.  Enter the organization name as : +++tffabrikam@lab.LabInstance.Id+++ enter the characters shown in your
    screen and then click on **Continue**.

    ![A screenshot of a computer AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image33.png)

7.  In the top right corner of the screen, click **User settings**. Click **Personal access tokens**.

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image34.png)

8.  Select **+ New Token**

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image35.png)

9.  Enter the name as : **devopstoken** and select the following scopes
    (you may need to select Show all scopes at the bottom of the page to
    reveal all scopes):

    - Agents Pool: **Read & write**

    - Build: **Read & execute**

    - Code: **Full**

    - Deployment Groups : Read & manage

    - GitHub Connections: Read & manage

    - Pipeline Resources: Use and manage

    - Project and Team: **Read, write, & manage**

    - Pull Request Threads: Read & write

    - **Secure Files: Read, create, & manage**

    - Release: **Read, write, execute, & manage**

    - Service Connections: **Read, query, & manage**

    - Team Dashboard: Read & manage

    - Task Groups: **Read, create, & manage**

    - **Test Management: Read & write**

    - Variable Groups: **Read, create, & manage**

    - **Work Items: Read, write, & manage**

    ![A screenshot of a computer AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image36.png)

10. Copy the generated API token and save it in a safe location. For
    your security, it won't be shown again.

    ![A screenshot of a computer AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image37.png)

### Task 5: Push Repo in Azure DevOps

1.  **Open GitBash from Desktop and run below command to navigate to the project repo.**

    +++cd "C:\LabFiles\azure-search-openai-demo"+++

    ![A screen shot of a computer AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image38.png)

2.	Replace you@example.com with your GitHub account and Your Name to be replaced with your Github account username in the below commands and run them.
   
    +++git config --global user.email "your email"+++

    +++git config --global user.name "Your Name"+++

    <img alt="image" src="https://github.com/user-attachments/assets/628fdb93-913a-4a2e-ae21-9cd47b11e38c" />

2.  Run below commands to push the repo.

    +++git init+++

    +++git add .+++

    +++git commit -m "Initial commit for migration lab"+++

    ![A screen shot of a computer program AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image39.png)

3.  Click on **Repos- > File*** from left navigation menu.

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image40.png)

4.  Under section **Initialize main branch with a README or gitignore** , select **Add a README** check box and **Python** from **Add a .gitignore ** drop down and then click on **Initialize.**

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image41.png)

5.  Switch back to GitBash and run below command to sign into Azure.
    Sign in with your Azure subscription account.

    +++az login+++

    ![A screen shot of a computer program AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image42.png)

    ![A screen shot of a computer program AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image43.png)

6.  Run below command to push local folder to Azure Devops. (Replace https://dev.azure.com/dev2gthubmigr/dev-github-proj/_git/dev-github-proj with your org link )

    +++git remote set-url origin https://dev.azure.com/dev2gthubmigr/dev-github-proj/_git/dev-github-proj+++

    **https://dev.azure.com/newdevorg123/newdev_proj/_git/dev-github-proj**

    ![A screen shot of a computer code AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image44.png)

7.  Run below commands to pull remote repos.

    +++git pull origin main --allow-unrelated-histories+++

8.  Run below command to push the repo to Devops. It prompts you to sign in. Iign in with your Devops account.

    +++git push -u origin --all+++

    ![A screenshot of a computer AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image45.png)

    ![A screenshot of a computer screen AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image46.png)

    ![A computer screen shot of a computer code AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image47.png)

    >[!note]**Note : If you already have repo in Devops then follow steps to pull and resolve conflict - 1. Pull from DevOps with unrelated history:** **git pull origin main --allow-unrelated-histories Step 2 : Resolve conflicts in files like .gitignore, README.md. Step 3 : Stage the resolved files - git add .**

    +++git commit -m "Resolved merge conflicts"+++

9.  Go back to Azure Devops project and check **Repos-\> Files**. You should see your repo here.

    ![A screenshot of a computer AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image48.png)

### Task 6: **Create a GitHub Personal Access Token (PAT)**

1.  Switch back to GitHub and click on **Settings**.

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image49.png)

2.  Click on **Developer Settings** from left navigation menu.

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image50.png)

3.  Click on **Personal Access Tokens->Tokens(classic)-> Generate new
    token(Classic)**

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image51.png)

4.  Enter the token name - **githubtoken-test** and keep all default values.

5.  Click on **Generate token -> Generate token**.

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image52.png)

6.  Copy the token and save it in notepad to use in next tasks.

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image53.png)

### Task 7: Perform Migration

1.  Switch back to GitBash. Run the following commands in your terminal
    (replace with your real tokens):

    +++export GH_PAT=ghp_yourgithubpat+++

    +++export AZURE_DEVOPS_PAT=youradopat+++

    +++export AZURE_DEVOPS_source_ORG=yourdevopsorg+++

    +++export AZURE_GITHUB_target_org=yourenterprisegithuborg+++

    ![](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image54.png)

2.  Run below command to provide migrator role

    +++gh gei grant-migrator-role --github-org devopstogtihub --actor chintharlamanjula --actor-type USER+++

    ![A screen shot of a computer code AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image55.png)

3.  Install the ado2gh CLI Extension

4.  Use the following command template to simulate the repo migration
    without copying data. You're telling GitHub Enterprise Importer
    (GEI) to **simulate** the migration, checking if everything is valid
    and ready to migrate - but **no actual repo, code, or history is
    transferred**.

5.  Replace **dev2gthubmigr** with your Azure DevOps **org name** with
    your org url and run the command and devopstogithub-org- your GitHub
    **org name**.

    ```gh ado2gh migrate-repo --ado-org dev2gthubmigr --ado-team-project dev-github-proj --ado-repo dev-github-proj --github-org devopstogtihub --github-repo dev-github-proj-migrated-trial --ado-pat $AZURE_DEVOPS_PAT --github-pat $GH_PAT --queue-only```

    ![A screen shot of a computer code AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image56.png)

    ```gh ado2gh wait-for-migration --migration-id RM_@lab.LabInstance.Id --github-pat $GH_PAT```

    ```gh ado2gh wait-for-migration --migration-id RM_kgDaACQxMjM5YzNkOC02MzFmLTRjM2EtODU2Yy02NDFmMWZiM2U2OTE --github-pat $GH_PAT```

    ![A screen shot of a computer code AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image57.png)

6.  Switch back to Github GEC -> organization and you should see repo

    ![A screenshot of a computer AI-generated content may be incorrect.](https:///raw.githubusercontent.com/technofocus-pte/mgrtdvopsghdepth/refs/heads/main/Lab01/media/image58.png)

### Summary

In this lab, you performed a trial simulation of migrating a source code
repository from Azure DevOps to GitHub Enterprise Cloud.  
You used the GitHub CLI along with the GitHub Enterprise Importer's
ado2gh extension to conduct a dry-run of the migration, ensuring the
process completes without errors before actual migration.

This hands-on walkthrough enabled you to:

- Authenticate with both ADO and GEC using PATs

- Configure your source (ADO) and target (GEC) environments

- Run and monitor a trial migration to validate readiness

- Gain confidence in using GEI tooling for future production migrations

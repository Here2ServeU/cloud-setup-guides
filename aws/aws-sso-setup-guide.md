###The Complete Beginner's Guide to Hosting This DocumentationThis guide assumes you have **Git** installed. If not, download it [here](https://www.google.com/search?q=https://git-scm.com/downloads).

####Step 1: Create the Repository on GitHub1. Log in to GitHub and click the **+** icon in the top-right corner.
2. Select **New repository**.
3. **Repository name:** Enter one of the titles above (e.g., `aws-sso-setup-guide`).
4. **Public/Private:** Choose **Public** (visible to everyone) or **Private** (only you can see it).
5. **Initialize this repository with:** Check the box that says **Add a README file**.
6. Click **Create repository**.

####Step 2: Clone (Download) the Repository to Your Computer1. On your new repository page, click the green **<> Code** button.
2. Copy the URL under the **HTTPS** tab.
3. Open your terminal (Command Prompt, PowerShell, or Terminal).
4. Type `git clone` followed by the URL you copied:
```bash
git clone https://github.com/YOUR-USERNAME/aws-sso-setup-guide.git

```


5. Move into that folder:
```bash
cd aws-sso-setup-guide

```



####Step 3: Create the Guide File1. Open this folder in your favorite text editor (like VS Code or Notepad).
2. Create a new file named `SETUP_GUIDE.md`.
3. **Copy and paste the content below** into that file and save it.

```markdown
# AWS IAM Identity Center (SSO) Setup Guide

## Overview
This guide documents the security best practices used to set up the `vest-deployer` user for the Vest Infrastructure project. Instead of long-term keys, we use IAM Identity Center for temporary, secure credentials.

## Phase 1: Cloud Setup (IAM Identity Center)
1.  **Create the User:**
    * Create a user in IAM Identity Center (e.g., `vest-deployer`).
2.  **Assign Access:**
    * Go to **AWS Accounts** -> Select Target Account (e.g., `7303-3527-6920`).
    * Assign the user to this account.
3.  **Define Permissions:**
    * Attach the **AdministratorAccess** permission set.
    * *Tip:* Set session duration to 12 hours to avoid frequent re-logins.

## Phase 2: Local CLI Configuration
1.  **Configure Profile:**
    Run the following command to create a named profile (isolates this project from others):
    ```bash
    aws configure sso --profile autumn-vest
    ```
2.  **Enter Details:**
    * **SSO Start URL:** (Get this from your IAM Identity Center Dashboard)
    * **SSO Region:** `us-east-1` (or your specific region)
    * **Registration Scopes:** Press `Enter` (default)
3.  **Authorize:**
    * The CLI will open your browser. Log in as `vest-deployer` and click **Allow**.

## Phase 3: Activation & Verification
To start working on the project, open your terminal and run:

### 1. Switch Context
Force the terminal to use your specific profile:
* **Mac/Linux:**
    ```bash
    export AWS_PROFILE=autumn-vest
    ```
* **Windows (PowerShell):**
    ```powershell
    $Env:AWS_PROFILE = "autumn-vest"
    ```

### 2. Verify Connection
Check that you are authenticated as the correct user on the correct account:
```bash
aws sts get-caller-identity
```
**Success Output:**
```json
{
    "UserId": "...:vest-deployer",
    "Account": "730335276920",
    "Arn": ".../vest-deployer"
}
```

```

####Step 4: Upload Your Changes to GitHubBack in your terminal (make sure you are still inside the folder), run these three commands one by one:

1. **Stage the file** (prepare it to be saved):
```bash
git add SETUP_GUIDE.md

```


2. **Commit the file** (save it with a message):
```bash
git commit -m "Add AWS SSO setup documentation"

```


3. **Push the file** (send it to GitHub):
```bash
git push origin main

```



####Step 5: Check Your WorkGo back to your GitHub repository page in your browser and refresh. You should now see `SETUP_GUIDE.md` in the file list. Click on it to see your beautifully formatted guide!

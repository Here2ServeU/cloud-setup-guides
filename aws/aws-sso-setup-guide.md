# How To Set Up AWS Single Sign-On (SSO)

Here is the step-by-step guide to setting up AWS Single Sign-On (SSO), now called **IAM Identity Center**, and connecting it to your CLI.

### Phase 1: Create the User (IAM Identity Center)

1. Log in to your AWS Management Console as the root user (or an admin).
2. Search for **IAM Identity Center** in the top search bar and open it.
3. *Note: If you haven't enabled it yet, click "Enable" (choose "Organization instance" if asked).*
4. In the left sidebar, click **Users**.
5. Click the orange **Add user** button.
6. **Specify user details:**
* **Username:** Enter a name (e.g., `t2s-deployer`).
* **Password:** Select "Generate a one-time password" (easiest for immediate setup) or "Send an email" (if setting it up for someone else).
* **Email address:** Enter your email.
* Fill in First name/Last name.
* Click **Next**.


7. **Add user to groups:** You can skip this for now. Click **Next**.
8. **Review:** Click **Add user**.
9. **Important:** A popup will appear with the **One-time password** and the **AWS access portal URL**. Copy these down; you will need them immediately to set your permanent password.

### Phase 2: Create a Permission Set

Before assigning the user to an account, you need to define *what* they can do (e.g., Administrator vs. Read Only).

1. In the IAM Identity Center sidebar, click **Permission sets**.
2. Click **Create permission set**.
3. Select **Predefined permission set**.
4. Choose **AdministratorAccess** (Best for your personal infrastructure projects).
5. Click **Next**.
6. **Session duration:** Change this from "1 hour" to **12 hours** (saves you from logging in constantly).
7. Click **Next**, then **Create**.

### Phase 3: Assign User to Account

Now you link the **User** + **Permission Set** + **Account**.

1. In the sidebar, click **AWS accounts**.
2. Check the box next to your AWS Account (e.g., `7197-3587-4967`).
3. Click **Assign users or groups**.
4. **Step 1:** Select the **Users** tab, check `vest-deployer`, and click **Next**.
5. **Step 2:** Select the **AdministratorAccess** permission set you just created, and click **Next**.
6. **Step 3:** Click **Submit**.

### Phase 4: Configure Local CLI

Now that the cloud side is ready, connect your terminal.

1. **Get your Start URL:**
* Go to the **Dashboard** in IAM Identity Center.
* Copy the **AWS access portal URL** (e.g., `https://<id>.awsapps.com/start`).


2. **Run the configuration command:**
Open your terminal and run:
```bash
aws configure sso

```


3. **Answer the prompts:**
* **SSO session name:** `vest-session` (or any name you like).
* **SSO start URL:** Paste the URL you copied.
* **SSO region:** `us-east-1` (or your specific region).
* **Registration scopes:** Press **Enter** (default).


4. **Authorize:**
* The CLI will open your browser.
* Log in with `vest-deployer` (use the password you set in Phase 1).
* Click **Allow**.


5. **Select Account:**
* Back in the terminal, use the arrow keys to select your account.
* Select the role **AdministratorAccess**.
* **CLI default client Region:** `us-east-1`.
* **CLI default output format:** `json`.
* **CLI profile name:** `autumn-vest` (Naming this profile is crucial to keep it separate).



### Phase 5: Verification 

To verify everything is working, run this command using your new profile:

```bash
aws sts get-caller-identity --profile autumn-vest

```

**Success:** You should see a response showing your User ID and ARN ending in `t2s-deployer`.

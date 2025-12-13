# Setting Up Secrets on GitHub To Deploy to AWS

### The "Hacker" Way (Fastest)

Since you already configured your CLI with the `t2s-cloud` profile, you can create the Robot user and get the keys in 3 commands without leaving your terminal.

1. **Create the Robot User:**
```bash
aws iam create-user --user-name t2s-github-bot --profile t2s-cloud

```


2. **Give it Admin Powers:**
```bash
aws iam attach-user-policy --user-name t2s-github-bot --policy-arn arn:aws:iam::aws:policy/AdministratorAccess --profile t2s-cloud

```


3. **Generate the Keys (Copy the Output!):**
```bash
aws iam create-access-key --user-name t2s-github-bot --profile t2s-cloud

```


* **Output:** You will see an `AccessKeyId` and a `SecretAccessKey`. **Copy these.**



---

### The Console Way (Visual)

If you prefer clicking through the website:

1. **Log in:** Go to your SSO Start URL and click **Management Console** next to your account `7379-1059-8753`.
2. **Go to IAM:** Search for "IAM" and click **Users**.
3. **Create User:**
* Click **Create user**.
* Name: `t2s-github-bot`.
* Click **Next**.


4. **Permissions:**
* Select **Attach policies directly**.
* Search for and check **AdministratorAccess**.
* Click **Next** > **Create user**.


5. **Get Keys:**
* Click on `vest-github-bot` in the list.
* Go to **Security credentials** tab.
* Click **Create access key** > Select **CLI** > **Next** > **Create**.
* **Copy the Access Key ID and Secret Access Key.**



---

### Add to GitHub (From your Screenshot)

Now that you have the keys (starts with `AKIA...` and `wJalr...`):

1. On the GitHub page you are viewing:
* Click the **Settings** tab (gear icon on the far right).
* On the left sidebar, look for **Security** -> Click **Secrets and variables** -> **Actions**.


2. Click the green **New repository secret** button.
3. Add these three secrets:

| Name | Value |
| --- | --- |
| **AWS_ACCESS_KEY_ID** | Paste the `AccessKeyId` from Step 1 or 2 |
| **AWS_SECRET_ACCESS_KEY** | Paste the `SecretAccessKey` from Step 1 or 2 |
| **AWS_REGION** | `us-east-1` |

Once you add these, your GitHub Actions will officially have permission to deploy to your AWS account!

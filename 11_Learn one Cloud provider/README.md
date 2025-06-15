# 🌐 AWS Account Setup with Security Best Practices

Securely launch your AWS Free Tier account with this step-by-step guide. You'll configure multi-factor authentication (MFA), create IAM users, set billing alarms, request SSL certificates, and personalize your IAM login — all following AWS best practices.

---

## 📑 Table of Contents

1. [Create AWS Free Tier Account](#1-create-aws-free-tier-account)
2. [Enable MFA for Root User](#2-enable-mfa-for-root-user)
3. [Create IAM User with Admin Access](#3-create-iam-user-with-admin-access)
4. [Set Up Billing Alarms](#4-set-up-billing-alarms)
5. [Request SSL Certificate via ACM](#5-request-ssl-certificate-via-acm)
6. [Customize IAM Login URL](#6-customize-iam-login-url)
7. [Security Recommendations](#7-security-recommendations)

---

## 1. ✅ Create AWS Free Tier Account

- Visit [AWS Free Tier](https://aws.amazon.com/free/)
- Click **“Create a Free Account”**
- Enter:

  - Email address
  - Account name
  - Strong root password (store in a password manager)

- Provide billing information (valid credit/debit card required)
- Complete phone verification
- Choose **“Basic Support”** plan (free)

---

## 2. 🔐 Enable MFA for Root User

1. Open the **IAM** service
2. Under _"Security recommendations"_, click **“Add MFA”**
3. Choose **Authenticator app** (e.g., Google Authenticator)
4. Scan the QR code with your mobile app
5. Enter two consecutive 6-digit codes
6. Click **“Add MFA”** to complete setup

---

## 3. 👤 Create IAM User with Admin Access

1. Go to **IAM → Users → Add user**
2. Fill in:

   - **Username**: `itadmin` (or preferred)
   - Enable **AWS Management Console access**
   - Choose **Autogenerate password**
   - Enable **password reset at next login**

3. **Permissions**:

   - Select **Attach policies directly**
   - Choose **AdministratorAccess**

4. Save credentials (CSV download)
5. Repeat MFA setup for this IAM user

---

## 4. 💰 Set Up Billing Alarms

### Enable Billing Preferences:

1. Go to **Billing Dashboard → Billing Preferences**
2. Enable:

   - ✅ Receive Free Tier alerts
   - ✅ Receive CloudWatch billing alerts

### Create Billing Alarm:

1. Open **CloudWatch** in **US East (N. Virginia)**
2. Go to **Alarms → Create Alarm**
3. Select:

   - Metric: **Billing > Total Estimated Charge**
   - Threshold: e.g., **\$5.00 USD**

4. Create an **SNS topic** (Simple Notification Service)

   - Enter your email address
   - Confirm email subscription from inbox

5. Name the alarm (e.g., `AWS Billing Alert`)

---

## 5. 🔒 Request SSL Certificate via ACM

1. Go to **Certificate Manager (ACM)**
2. Click **“Request a certificate”**
3. Choose **Request a public certificate**
4. Enter domain: `*.yourdomain.com`
5. Select **DNS Validation**
6. In your domain registrar’s DNS panel:

   - Add a **CNAME record**
   - Name: strip domain portion from the provided name
   - Value: paste the full value from ACM

7. Wait for certificate validation (may take up to 48 hours)

---

## 6. 🌐 Customize IAM Login URL

1. In **IAM Dashboard**, click **“Customize”** under **IAM users sign-in link**
2. Enter alias (e.g., `yourcompany`)
3. Your login URL becomes:
   `https://yourcompany.signin.aws.amazon.com/console`
4. Test IAM login:

   - Use credentials from CSV
   - Change password on first login
   - Enter MFA code when prompted

---

## 7. 🔒 Security Recommendations

- Avoid using the **root user** for daily tasks
- **Never share** root credentials or access keys
- Enable **MFA** for all IAM users
- Store passwords and credentials in a **secure password manager**
- **Review billing dashboard** regularly
- **Delete unused resources** to avoid unexpected charges
- Keep your contact information updated for billing alerts

---

> ⚠️ AWS charges may apply if usage exceeds Free Tier limits. Monitor your usage regularly!

---

# 🧾 **AWS Beginner Setup Notes – Free Tier Safe Setup**

## ✅ **PHASE 1: Safe AWS Account Setup (Free Tier Friendly)**

---

### 🔹 Step 1: Create AWS Account

* Visit [https://aws.amazon.com/free](https://aws.amazon.com/free)
* Sign up with:

  * Email
  * Root account username
  * Password
* Enter contact details (choose **Personal Account**)
* Add a **credit/debit card** (₹2 refundable hold may be applied)
* Choose support plan: ✅ **Basic Support – Free**

🔐 AWS may ask for:

* **PAN** – required for Indian users
* **Consent for third-party identity verification** – must accept

✅ Account takes a few minutes to activate. AWS sends a confirmation email.

---

### 🔹 Step 2: Initial AWS Console Setup

Once logged in to [https://console.aws.amazon.com](https://console.aws.amazon.com):

* Set region (default): ✅ **US East (N. Virginia)** `us-east-1` (important for billing metrics)
* Explore services like EC2, S3, Lambda

---

### 🔹 Step 3: Enable Free Tier Alerts

1. Go to:
   **Search bar → Billing → Billing Preferences**
2. ✅ Check: **“Receive Free Tier Usage Alerts”**
3. Enter your email address
4. Click **Save Preferences**

---

### 🔹 Step 4: (Optional but Recommended) Enable Cost Explorer

1. Go to:
   **Billing → Cost Explorer**
2. Click **“Enable”**

This shows usage and cost breakdowns.

---

### 🔹 Step 5: Create an IAM Admin User (For Daily Use)

1. Go to:
   **Search bar → IAM → Users → Add User**

2. User Details:

   * User name: `mn-admin` (or anything)
   * ✅ Enable: **AWS Management Console access**
   * Set a **custom password**
   * ❌ Uncheck “Require password reset”

3. Set Permissions:

   * Choose: **Attach policies directly**
   * ✅ Select: **AdministratorAccess**

4. Skip tags → Click **Create user**

✅ AWS will show your **IAM login URL** — save it.

> Use this IAM user for all future logins
> Never use root account for daily tasks

---

### 🔹 Step 6: Set Up CloudWatch Billing Alarm (Optional – Once Available)

⏳ Billing metrics may take **12–24 hrs** to appear after account setup.

Once available:

1. Go to:
   **CloudWatch → Alarms → Create Alarm**

2. Select Metric:

   * Click **Browse**
   * Choose: **Billing → TotalEstimatedCharge**
   * Select: **EstimatedCharges (USD or INR)**

3. Set Condition:

   * “Greater than” → `0.01`

4. Notification:

   * Create SNS topic: `BillingAlertTopic`
   * Enter your email
   * Click **Create topic**
   * ✅ Confirm email subscription from inbox

5. Name alarm: `AWSBillingAlarm`

6. Click **Create Alarm**

🔔 You’ll now be alerted by email if your AWS charges go over \$0.01

---

## 📘 Concepts You Learned

| Concept            | Description                                                               |
| ------------------ | ------------------------------------------------------------------------- |
| **Root User**      | Superuser with unrestricted access — use only for billing/account changes |
| **IAM User**       | Safer, controlled user for daily AWS use                                  |
| **Free Tier**      | Limited usage of services (e.g., EC2, S3, Lambda) at no cost              |
| **Billing Alerts** | Email warnings when approaching/exceeding Free Tier                       |
| **CloudWatch**     | AWS service for monitoring metrics, alarms, and logs                      |
| **SNS Topic**      | Used by CloudWatch to send email notifications                            |


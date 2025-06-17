# ☁️ Amazon EC2 (Elastic Compute Cloud) - Full Beginner Guide & Hands-On Summary

---

## ✅ What is Amazon EC2?

**EC2** (Elastic Compute Cloud) is a core AWS service that allows you to run virtual machines (called **instances**) in the cloud. You can install applications, host websites, run Java apps, etc., just like you do on your local laptop — but on cloud infrastructure.

---

## 🔹 Why use EC2?

* Run apps without buying physical servers
* Easily scale (increase/decrease capacity)
* Pay only for what you use
* Full control over your OS and software stack
* Integrate with other AWS services

---

## 🔰 Step-by-Step Guide: Launching and Using EC2

### 1. **Sign In as IAM User**

* Use IAM user for daily tasks (not Root account).
* Root account has full access — if compromised, it's a big risk.
* IAM user has **limited permissions**, making it safer.
* You can delete or rotate IAM user credentials if needed.

---

### 2. **Go to EC2 Dashboard**

* AWS Console → EC2 → Launch Instance

---

### 3. **Configure Your EC2 Instance**

#### 🖥️ a) **Choose AMI (OS)**

* We used:
  **Ubuntu Server 22.04 LTS (HVM), SSD Volume Type**
  ✅ Free-tier eligible
  ✅ Verified provider
  ✅ 64-bit x86

---

#### 🧠 b) **Choose Instance Type**

* **t2.micro**
  ✅ 1 vCPU
  ✅ 1 GB RAM
  ✅ Free-tier eligible

---

#### 🔐 c) **Create Key Pair (.pem file)**

* Used for SSH login to instance securely
* We downloaded it and kept it in:
  `~/Downloads/malobika-key.pem`
  👉 Store it safely and **don’t lose it**

---

#### 🌐 d) **Network Settings (VPC, Subnet, Public IP, Security Group)**

* ✅ VPC: default
* ✅ Subnet: auto
* ✅ Public IP: **enabled**
* ✅ Security Group: created new with rules:

| Type   | Port | Source    | Purpose             |
| ------ | ---- | --------- | ------------------- |
| SSH    | 22   | My IP     | To connect via SSH  |
| HTTP   | 80   | 0.0.0.0/0 | To serve websites   |
| Custom | 8080 | 0.0.0.0/0 | For Spring Boot app |

---

### 4. **Launch the Instance**

* EC2 instance launched!
* It has a **Public IPv4 Address** to access it over the internet
* You can **Start**, **Stop**, or **Terminate** instance anytime

---

## 🛠️ SSH into EC2 from Mac Terminal

```bash
cd ~/Downloads
chmod 400 malobika-key.pem

ssh -i "malobika-key.pem" ubuntu@<your-public-ip>
```

🟢 Now you're inside the EC2 instance (like a remote terminal)

---

## 🚀 Deploy Your Java App to EC2

1. Copy JAR file from your Mac to EC2:

```bash
scp -i "malobika-key.pem" /path/to/your.jar ubuntu@<public-ip>:/home/ubuntu/
```

2. Inside EC2, run the app:

```bash
java -jar your-app.jar
```

✔️ Your Spring Boot app is now running on the cloud!

---

## 🛑 Stopping the Instance

* You can **stop** your EC2 instance when not using it:

  * Saves compute charges
  * Keeps EBS volume (disk) with your data
* Still incur **small storage charges** (e.g. ₹8–₹10/month for 8 GB) — within free tier

---

## 🗑️ Terminating the Instance (Optional)

* Deletes EC2 + deletes the attached **EBS storage**
* This frees all costs but also **erases all your app/data**

---

## 💡 Quick Notes

* Always **stop** instances when not using them
* Don't **delete your `.pem` file** — you'll lose access
* Use `t2.micro` + Free Tier AMIs to avoid charges
* Use **Elastic IP** if you want a fixed IP address
* You can install any software via `apt`, `java`, etc.

---

## 🔄 Recap Checklist

✅ IAM user login
✅ Launch EC2 with Ubuntu
✅ Configure key pair and security groups
✅ SSH into instance
✅ Deploy and run Spring Boot app
✅ Stop instance when done

---

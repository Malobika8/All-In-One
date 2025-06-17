## 🧠 What is S3?

**Amazon S3 = Cloud-based file storage**
Think of it like **Google Drive** or **Dropbox**, but for developers and applications.

You can use it to:

* Store files (images, PDFs, logs, backups, videos, etc.)
* Serve files to apps and users
* Host static websites
* Store unlimited data (scales automatically)

---

## 📦 Core Concepts in S3

| Concept                   | Meaning                                                     |
| ------------------------- | ----------------------------------------------------------- |
| **Bucket**                | Like a folder or drive in the cloud                         |
| **Object**                | Any file you upload (image, PDF, text, etc.)                |
| **Key**                   | The full path + filename (like `/folder1/photo.jpg`)        |
| **Region**                | Where the bucket is physically located                      |
| **Storage Class**         | Determines cost & durability (we’ll use “Standard” for now) |
| **Public/Private Access** | By default, all files are private unless made public        |

---

## ✅ Free Tier (Very Generous)

* **5 GB of Standard Storage**
* **20,000 GET requests**
* **2,000 PUT requests per month**

Plenty for learning and small apps — totally safe.

---

## 📌 Step-by-Step: Create Your First S3 Bucket

Before we upload files, we need to **create a bucket** — your own cloud folder.

### 🟢 Step 1: Go to S3 Service

1. In the AWS Console (logged in as IAM user)
2. In the **top search bar**, type:
   👉 `S3`
3. Click on **“S3 – Scalable Storage in the Cloud”**

---

### 🟢 Step 2: Create Bucket

1. Click the **orange “Create bucket”** button (top right)

2. Fill in the details:

| Field                                     | Value                                                                  |
| ----------------------------------------- | ---------------------------------------------------------------------- |
| **Bucket name**                           | Use a unique name like `malobika-s3-test` (must be globally unique)    |
| **Region**                                | Leave as default (`US East (N. Virginia)`)                             |
| **Block Public Access**                   | ✅ Leave all boxes **checked** (default) for now – keeps bucket private |
| **Bucket versioning**                     | ❌ Disabled (we’ll skip for now)                                        |
| **Tags / Encryption / Advanced Settings** | Leave as-is                                                            |

3. Click **“Create bucket”** (bottom of the form)

---

## Let’s put something inside it — like a file, image, or text document — and explore how storage works in AWS S3.

---

## 📂 Step-by-Step: Upload a File to Your S3 Bucket

### 🟢 Step 1: Go to Your Bucket

1. From the S3 dashboard, click on your bucket name
   (e.g., `malobika-s3-test`)

---

### 🟢 Step 2: Upload a File

1. Click the **“Upload”** button

2. In the upload panel:

   * Click **“Add files”**
   * Choose any small file from your computer (e.g., `test.txt`, `image.jpg`)

> 📁 Tip: Upload something safe and small — Free Tier allows 5 GB total

3. Scroll down to **"Permissions" section**

   * ✅ Leave as-is (**private** by default)

4. Click **“Upload”** (bottom of page)

---

### 🎯 What Just Happened?

* Your file is now stored in the cloud, inside your bucket.
* This file is called an **object**
* It has a unique **key** (name + path) inside your bucket

---

## 🔍 Step 3: View the Uploaded Object

1. Once upload finishes, click on the file name in your bucket
2. You’ll see details like:

   * **Object URL**
   * **Size**
   * **Storage class**
   * **Permissions**

> 🔒 The object is **private by default**, meaning **only you (the account owner)** can access or download it.

# FYI 

You're seeing:

> **“Bucket policy changes can’t be saved… conflicts with your Block Public Access settings”**

Which means:

* Your **bucket has "Block Public Access" fully enabled**
* And AWS is **blocking any attempt to make things public** — even through a policy

---

## 🛠️ Fix This: Update Block Public Access Settings

Here’s how to allow public access **safely and intentionally** so you can continue:

---

### ✅ Step-by-Step: Allow Public Access for This Bucket

1. Go to:
   **S3 Console → Your Bucket → Permissions tab**

2. Scroll to:
   🔐 **“Block public access (bucket settings)”**

3. Click: **Edit**

4. Uncheck:
   ✅ **“Block all public access”**

> AWS will show a warning — that’s okay for learning purposes.

5. Confirm by typing **"confirm"** in the box, if prompted

6. Click **Save**

---

### 🔁 Then Retry Adding the Bucket Policy

Now go back to:

* **Bucket policy section**
* Paste the same public read policy again:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowPublicReadAccessToAllObjects",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```

👉 Replace `your-bucket-name` with your actual bucket name
Click **Save**

---

### ✅ Finally:

Go to your file → copy the **Object URL** → open in **incognito/private window**

You should now see the file load in your browser.

---


Let’s now turn our S3 bucket into a **static website host** — like a mini version of Netlify or GitHub Pages.

We’ll be able to access our HTML site using a **public link**, directly from AWS.

---

## 🌐 What Is a Static Website?

A **static website** is made of plain files:

* `.html`, `.css`, `.js`, `.jpg`, etc.
* No server-side code (like Java, PHP)

> S3 lets you host static websites **very cheaply** or even **entirely free** within the free tier.

---

## ✅ What we’ll Do Now

We’ll configure our bucket to:

1. Allow public access
2. Enable static website hosting
3. Upload an `index.html` file
4. Access the site via a public URL

---

## 🟢 Step-by-Step: Host a Static Website on S3

---

### ✅ Step 1: Prepare an `index.html` File

Create a basic HTML file on your computer:

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
<head>
  <title>Welcome</title>
</head>
<body>
  <h1>Hello from Malobika’s AWS S3 Static Website!</h1>
  <p>This is a test static site hosted on S3.</p>
</body>
</html>
```

Save it as `index.html` locally.

---

### ✅ Step 2: Upload `index.html` to Your Bucket

1. Go to **S3 → Your Bucket**
2. Click **Upload**
3. Add your `index.html` file
4. ✅ Leave permissions as-is (we already enabled public access earlier)
5. Click **Upload**

---

### ✅ Step 3: Enable Static Website Hosting

1. In your **bucket**, click **Properties** tab

2. Scroll to **Static website hosting**

3. Click **Edit**

4. Select:

   * ✅ **Enable**
   * **Index document**: `index.html`
   * (Optional) **Error document**: `error.html` (if you have one)

5. Click **Save changes**

✅ You’ll now see a **“Bucket website endpoint”** — copy that URL.

---

### ✅ Step 4: Visit Your Static Website

Paste that endpoint into your browser.
🎉 You should see your HTML page served live from S3!

---

## 🧠 Notes

| Concept                                 | Info                                         |
| --------------------------------------- | -------------------------------------------- |
| S3 hosting is only for static content   | No Java/Spring Boot/etc.                     |
| Free tier gives 5 GB + 20,000 views     | Totally enough for practice and personal use |
| You can host entire frontend sites here | HTML, CSS, JS, React builds, etc.            |

---

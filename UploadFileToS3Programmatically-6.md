Upload a file to S3 using code — you’ll need:

1. AWS access credentials (from an IAM user)
2. AWS SDK (Java or Python)
3. A configured region and bucket

---

## 🟢 Java Example: Upload File to S3

### ✅ Prerequisites:

* Java project with Maven
* AWS SDK for Java
* AWS access key + secret key
* Target bucket name and file

---

### 🔧 Step 1: Add AWS SDK to `pom.xml`

```xml
<dependency>
  <groupId>software.amazon.awssdk</groupId>
  <artifactId>s3</artifactId>
  <version>2.21.30</version> <!-- Use latest -->
</dependency>
```

---

### 🔐 Step 2: IAM Access Keys

Go to:

* **IAM → Users → Your IAM user → Security credentials tab**
* Click: **Create access key**
* Note the **Access Key ID** and **Secret Access Key**

⚠️ Keep them private.

---

### 🔧 Step 3: Java Code (Upload File)

```java
import software.amazon.awssdk.auth.credentials.AwsBasicCredentials;
import software.amazon.awssdk.auth.credentials.StaticCredentialsProvider;
import software.amazon.awssdk.regions.Region;
import software.amazon.awssdk.services.s3.S3Client;
import software.amazon.awssdk.services.s3.model.PutObjectRequest;
import java.nio.file.Paths;

public class S3Uploader {
    public static void main(String[] args) {
        String bucketName = "your-bucket-name";
        String keyName = "uploaded-file.txt"; // file name in S3
        String filePath = "/path/to/local/file.txt"; // local file path

        AwsBasicCredentials awsCreds = AwsBasicCredentials.create(
            "YOUR_ACCESS_KEY_ID",
            "YOUR_SECRET_ACCESS_KEY"
        );

        S3Client s3 = S3Client.builder()
            .region(Region.US_EAST_1) // or Region.of("ap-south-1")
            .credentialsProvider(StaticCredentialsProvider.create(awsCreds))
            .build();

        s3.putObject(
            PutObjectRequest.builder()
                .bucket(bucketName)
                .key(keyName)
                .build(),
            Paths.get(filePath)
        );

        System.out.println("File uploaded successfully.");
    }
}
```

---

## ✅ Output:

> File is uploaded to:
> `https://your-bucket-name.s3.amazonaws.com/uploaded-file.txt`

(if public access or website hosting is enabled)

---

## 🔐 Security Tip

* Don’t hardcode credentials in real apps
* Use **`~/.aws/credentials`** file or **environment variables** for production
* Add retry logic and error handling for robustness

We’ll fix three important things:

---

## ✅ 1. **Don’t Hardcode AWS Credentials**

Never do this in real projects:

```java
AwsBasicCredentials.create("ACCESS_KEY", "SECRET_KEY") // ❌ bad practice
```

### ✅ Instead: Use `~/.aws/credentials` file (recommended by AWS SDK)

---

### 📂 Step-by-Step: Use `~/.aws/credentials`

#### 🛠 Step 1: Create the file (if it doesn’t exist)

📍 Path:

* **Windows**: `C:\Users\<your-username>\.aws\credentials`
* **Mac/Linux**: `~/.aws/credentials`

#### 📝 Content:

```ini
[default]
aws_access_key_id = YOUR_ACCESS_KEY
aws_secret_access_key = YOUR_SECRET_KEY
```

(Replace with your IAM user credentials)

---

#### 🛠 Step 2: Use the Default Credential Provider in Java

✅ Change your Java code to:

```java
S3Client s3 = S3Client.builder()
    .region(Region.US_EAST_1) // Or ap-south-1
    .build(); // No need to manually provide credentials!
```

Now AWS SDK will **automatically load credentials** from:

* `~/.aws/credentials`
* Or environment variables (`AWS_ACCESS_KEY_ID`, etc.)
* Or instance role (if in EC2)

---

## ✅ 2. Use Environment Variables (Alternate Method)

### 🧪 Use this for temporary apps, CI/CD pipelines, or Docker

Set these:

```bash
export AWS_ACCESS_KEY_ID=your_access_key
export AWS_SECRET_ACCESS_KEY=your_secret_key
```

And the SDK will pick them up automatically — no code change needed.

---

## ✅ 3. Add Retry Logic & Error Handling

Let’s make your upload **fail-safe**:

```java
try {
    s3.putObject(
        PutObjectRequest.builder()
            .bucket(bucketName)
            .key(keyName)
            .build(),
        Paths.get(filePath)
    );
    System.out.println("✅ Upload successful.");
} catch (S3Exception e) {
    System.err.println("❌ Upload failed: " + e.awsErrorDetails().errorMessage());
    // retry logic here if needed
} catch (IOException e) {
    System.err.println("❌ File error: " + e.getMessage());
}
```

---

### 💡 Optional: Use AWS SDK’s Built-in Retry Config

The AWS Java SDK v2 already **retries failed requests automatically**, but you can customize it like this:

```java
import software.amazon.awssdk.core.client.config.ClientOverrideConfiguration;
import software.amazon.awssdk.core.retry.RetryPolicy;

S3Client s3 = S3Client.builder()
    .region(Region.US_EAST_1)
    .overrideConfiguration(ClientOverrideConfiguration.builder()
        .retryPolicy(RetryPolicy.defaultRetryPolicy())
        .build())
    .build();
```

---

## ✅ Summary

| Goal                           | How                                   |
| ------------------------------ | ------------------------------------- |
| 🚫 Avoid hardcoded credentials | Use `~/.aws/credentials` or env vars  |
| 🔁 Retry failed requests       | SDK auto-retries; customize if needed |
| ⚠️ Add proper error messages   | Catch `S3Exception`, `IOException`    |
| ✅ Keep code clean              | Let SDK handle auth securely          |


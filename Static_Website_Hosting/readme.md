# 🚀 Deploy Static Website on AWS S3

## 📌 Step 1: Create an S3 Bucket for Website Hosting

1. Open the AWS S3 Console and click **Create bucket**.

2. **Bucket Name**  
   Enter your domain name (e.g., example.com).

3. **Region**  
   Select your preferred AWS region.

4. **Disable Block Public Access**  
   - Uncheck **Block all public access**  
   - Confirm the changes.

5. **Enable Static Website Hosting**
   - Go to the **Properties** tab.
   - Click **Edit** under Static website hosting.
   - Select:
     - Enable  
     - Host a static website
   - Set **Index document** as:
     ```
     index.html
     ```
   - Note the **Bucket Website Endpoint URL**.
   - Save changes.

6. Click **Create bucket**.

---

## 📌 Step 2: Upload Website Files

1. Open your S3 bucket.

2. Click **Upload → Add files**

3. Upload your files:
   - index.html
   - style.css
   - script.js
   - images (if any)

4. Click **Upload**

---

## 📌 Step 3: Add Bucket Policy for Public Access

Add the following bucket policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadAccess",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}

## 🌐 Access Your Website

Use the S3 Website Endpoint URL: http://your-bucket-name.s3-website-region.amazonaws.com

---

## ✅ Notes

- Make sure `index.html` is present in the bucket  
- Public access must be enabled (Block Public Access disabled + bucket policy added)  
- Upload files directly inside the bucket (do not upload as a zip file)
``



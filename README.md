# 🔐 Project 4A – Secure OTT Video Streaming using CloudFront Signed URLs

This project demonstrates how to securely deliver private OTT video content using **AWS CloudFront Signed URLs**, ensuring that users can access the video only within a limited time frame.

---

## 🎯 Objective

Build a secure video delivery pipeline that:

- Makes all video content in Amazon S3 private
- Uses **CloudFront + OAC** to serve the content
- Restricts access using **Signed URLs** generated via a CloudFront Key Pair
- Ensures playback is valid only for a specific duration (e.g., 10 minutes)

---

## 🧰 AWS Services Used

| Service | Role in the Project |
|--------|----------------------|
| **Amazon S3** | Stores private `.mp4` video file |
| **CloudFront** | Distributes video securely via CDN |
| **Origin Access Control (OAC)** | Grants CloudFront permission to access S3 |
| **IAM** | Used to manage permissions and policies |
| **CloudFront Key Group** | Used for signing and verifying URL tokens |
| **Python (Boto3 + rsa)** | Scripted the generation of signed URLs |

---

## 🔐 Secure Streaming Flow

1. Upload `.mp4` to a private S3 bucket (block all public access)
2. Create a CloudFront distribution with OAC and connect it to S3
3. Generate a CloudFront **Key Pair** and **Key Group**
4. Write a Python script using `boto3` + `rsa` to create signed URLs
5. Embed the signed URL in a player (or open directly)
6. After expiration (e.g., 10 minutes), playback fails with `Access Denied`

---

## 🧪 Testing the Signed URL

- 🔄 **Before expiry**: Video streams successfully from CloudFront
- ⛔ **After expiry**: Link returns HTTP 403 Forbidden (as expected)
- 🕵️ **URL format**:  https://d3o3w9cskw6rvc.cloudfront.net/sample.mp4?Expires=175122704&Signature=Bw7T6Ln33********_&Key-Pair-Id=pk-APK********

# 🔐 DevSecOps Access & Security Concepts

## 📘 Introduction

This document is part of my **DevOps Security learning journey**, designed to help engineering managers and DevOps professionals understand the key authentication, authorization, and encryption concepts that secure modern systems. Each concept is explained simply yet technically, with real-world DevOps examples.

---

## 1. **OAuth (Open Authorization)**

### 🎯 Concept

OAuth is an **authorization protocol** that allows one application to access specific data from another service **without sharing the user’s password**.

For example:

> When you log in to a website using “Login with Google,” the site gets an access token from Google that allows it to read your email, but it never sees your password.

---

### ⚙️ Technical Principle

* The user asks a client app to access data from a resource server.
* The client requests authorization from an **Authorization Server** (e.g., Google).
* The user consents → the server issues an **Access Token**.
* The client uses this token to access the resource.

**Token Types:**

* **Access Token:** Short-lived access.
* **Refresh Token:** Used to get a new access token.

---

### 🧠 DevOps Example

In a **Jenkins CI/CD pipeline**, you can connect to GitHub using an **OAuth token** instead of storing your GitHub password, improving security.

---

### ⚖️ Quick Comparison

| Concept        | Purpose                       | Deals With    |
| -------------- | ----------------------------- | ------------- |
| OAuth          | Authorization                 | Access Tokens |
| OpenID Connect | Authentication built on OAuth | ID Tokens     |

---

## 2. **SSO (Single Sign-On)**

### 🎯 Concept

SSO allows a user to **log in once** and gain access to multiple systems or applications without logging in again.

For example:

> Logging into Gmail automatically gives access to Google Drive, YouTube, and other Google apps.

---

### ⚙️ Technical Principle

* Uses an **Identity Provider (IdP)** such as Azure AD or Okta.
* All connected applications trust the same IdP.
* The IdP issues a **session token** after the first successful login, reused across systems.

---

### 🧠 DevOps Example

In an enterprise setup:

* SSO enables seamless access for engineers to **Jenkins, GitLab, Grafana, AWS Console**, and other tools using the same corporate identity.

---

### ⚖️ OAuth vs SSO

|             | OAuth                      | SSO                             |
| ----------- | -------------------------- | ------------------------------- |
| Purpose     | Authorization between apps | Unified login for users         |
| Type        | Protocol                   | Solution (may use OAuth/OpenID) |
| Interaction | App ↔ App                  | User ↔ Multiple systems         |

---

## 3. **IAM (Identity and Access Management)**

### 🎯 Concept

IAM is a **framework for managing identities and permissions** in an organization or cloud platform (e.g., AWS IAM).

> It defines who can do what, where, and how.

---

### ⚙️ Technical Components

* **Users:** Human accounts.
* **Groups:** Collections of users.
* **Roles:** Temporary or assignable access permissions.
* **Policies:** JSON rules defining permissions (e.g., “Allow s3:GetObject”).

---

### 🧠 DevOps Example

In AWS:

* Create an **IAM Role** for Jenkins to deploy resources securely without embedding credentials.

```json
{
  "Effect": "Allow",
  "Action": ["s3:PutObject"],
  "Resource": "arn:aws:s3:::my-deploy-bucket/*"
}
```

---

## 4. **Encryption**

### 🎯 Concept

Encryption is the process of **converting readable data into an unreadable format**, only reversible using a decryption key.

---

### ⚙️ Types of Encryption

| Type           | Description                            | Examples     |
| -------------- | -------------------------------------- | ------------ |
| **Symmetric**  | Same key for encryption and decryption | AES, DES     |
| **Asymmetric** | Public + private key pair              | RSA, ECC     |
| **Hashing**    | Irreversible fixed-length value        | SHA-256, MD5 |

---

### 🧠 DevOps Example

* Jenkins encrypts stored secrets using **AES**.
* GitHub Actions stores **encrypted secrets** for pipelines.
* HTTPS certificates use **asymmetric encryption** to secure client-server traffic.

---

### 🔐 Practical Example

```bash
# Encrypt a file (Symmetric Encryption)
openssl enc -aes-256-cbc -in secret.txt -out secret.enc

# Decrypt it
openssl enc -d -aes-256-cbc -in secret.enc -out secret.txt
```

---

## 🚀 Summary Table

| Concept    | Purpose         | Real Use Case             | Common Tools               |
| ---------- | --------------- | ------------------------- | -------------------------- |
| OAuth      | Authorization   | Login with Google         | GitHub OAuth, Spotify API  |
| SSO        | Unified Login   | Office 365, Okta          | Azure AD, Google Workspace |
| IAM        | Access Control  | AWS IAM Roles             | AWS, GCP, Azure            |
| Encryption | Data Protection | HTTPS, Secrets Management | OpenSSL, KMS, Vault        |



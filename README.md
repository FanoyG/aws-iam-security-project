# 🚀 AWS IAM Security Project

This project demonstrates how to securely configure AWS Identity and Access Management (IAM) using best practices, including user creation, group policies, MFA setup, CLI configuration, and enforcing the principle of least privilege.

---

## 🎯 Objective

Set up a secure IAM environment in AWS Cloud by:

- Avoiding the use of the root account for daily operations  
- Creating IAM users with appropriate roles  
- Applying least privilege access control  
- Enabling MFA  
- Testing and verifying access using AWS CLI  

---

## 🛠️ Tasks Completed

### ✅ 1. Avoid Using Root Account
- Root account was used only once to set up the first admin user.  
- **MFA enabled** on the root account for added security.

### ✅ 2. Create an IAM Admin User
- Created user `Fanoy` with full administrator access.  
- Attached `AdministratorAccess` managed policy.  
- Login access enabled with password.  
- MFA configured using **Authy** app.

### 🛠️ Step 3: Create IAM Groups, Users, and Roles  
*(Detailed configuration files available in the `policies/` folder)*

- ✅ **Create IAM Groups**  
  - **AdminGroup**: Full admin access (`AdministratorAccess` AWS managed policy)  
  - **DevGroup**: Developer group with EC2 and S3 access (custom policy)  
  - **AuditGroup**: View-only permissions (`SecurityAudit` AWS managed policy)  

- ✅ **Create IAM Users and Assign to Groups**

| User    | Group       | Role             | MFA | Notes                         |
|---------|-------------|------------------|-----|-------------------------------|
| alice   | AdminGroup  | Senior Admin     | Yes | Full access user              |
| bob     | DevGroup    | Junior Developer | Yes | Has EC2 and S3 access        |
| charlie | DevGroup    | Intern Developer | Yes | DevGroup + inline deny policy |
| david   | AuditGroup  | Security Auditor | Yes | View-only access             |

- ✅ **Attach Policies**

  - **AdminGroup**: Attached AWS managed policy `AdministratorAccess`  
  - **DevGroup**: Attached custom policy allowing full EC2 and S3 access  
  - **AuditGroup**: Attached AWS managed policy `SecurityAudit`  

- ✅ **Add Inline Policy (For Intern Restriction)**  
  - Inline policy attached to `charlie` denying EC2 instance termination  
  - Example inline deny policy available in `intern-inline-policy.json`

- ✅ **Create IAM Roles (Optional but Recommended)**  
  - Created EC2 Role (e.g., `EC2S3ReadOnlyRole`) with read-only S3 access  
  - Demonstrated how EC2 instances can assume this role  

---

### ✅ 4. Apply Least Privilege Access
- Tested policies for:  
  - Alice: Full access  
  - Charlie: Blocked EC2 termination  
  - David: View-only access  
- Demonstrated differences between group, managed, and inline policies.

### ✅ 5. Enable MFA for All IAM Users
- Configured virtual MFA using **Authy** for all users.  
- Planned recovery strategy for lost devices.

### ✅ 6. AWS CLI Configuration
- Configured CLI with named profiles for each user.  
- Tested commands such as:  
  - `aws s3 ls`  
  - `aws ec2 describe-instances`  
  - `aws iam list-users`

---

## 💻 Folder Structure

📦 aws-iam-security-demo  
┣ 📜 README.md  
┣ 📂 screenshots  
┃ ┣ 📜 root-mfa-enabled.png  
┃ ┣ 📜 iam-admin-user.png  
┃ ┗ 📜 group-policy-example.png  
┣ 📂 cli-commands  
┃ ┗ 📜 mfa-setup-and-test.sh  
┗ 📂 policies  
  ┣ 📜 developer-group-policy.json  
  ┣ 📜 intern-inline-policy.json  
  ┗ 📜 admin-full-access.json  

---

## 🔐 Security Best Practices Demonstrated

- Root account locked down and protected with MFA.  
- Least privilege model enforced using groups and policies.  
- MFA configured across all users.  
- Clear demonstration of inline vs managed policies.

---


## 🧪 Testing (via AWS CLI)

Tested permissions using:  
- `aws configure --profile alice`  
- `aws s3 ls` → verified read-only access  
- `aws iam create-user` → blocked for Alice (no permission)  

---

## 🙌 Author

**Fanoy** - Aspiring Cloud Engineer 🚀  
Connect with me on [LinkedIn](https://www.linkedin.com/in/adil-khan-9b9860282/)  
Project hosted on [GitHub](https://github.com/your-username/aws-iam-security-project)

---

## 📌 Notes

This project was created as a real-world hands-on implementation to showcase IAM configuration, security hardening, and automation on AWS.

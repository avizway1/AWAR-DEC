### **Steps to Create an AWS Account**

### **Step 1: Provide Root User Email and Account Name**  
1. Go to the AWS console webpage https://aws.amazon.com/console.  
2. Enter your **root user email address** (the email ID you will use as the primary login for your AWS account).  
3. Provide an **account name** (e.g., "My AWS Account"/ "Prod" / "UAT" / "Dev" / "Training").  
4. Verify your email:  
   - AWS will send a **verification code** to the provided email address.  
   - Enter the code in the signup form to verify the email address.  
5. Set up a **strong password** for your account to secure access.  

---

### **Step 2: Provide Contact Information**  
1. Choose the **account type**:  
   - **Business** (recommended for organizational use).  
   - **Personal** (suitable for individual use or learning purposes). 
2. Enter your **contact information**:  
   - Full Name  
   - Phone Number  
   - Address  
   - Country/Region  

---

### **Step 3: Enter Billing Information**  
1. Provide valid **credit or debit card information** for payment verification.  
2. Ensure the **billing details match the account information** (name and address) to avoid potential account suspension.  
3. AWS will deduct a small amount for verification:  
   - Example: **₹2 INR** or **$1 USD**.  
   - This amount will be refunded after validation.  

**Tip:** Provide same name in step 2 and payment information.  
**Tip:** make sure you enable International transaction.  

---

### **Step 4: Confirm Identity**  
1. **Select your country** to confirm your location.  
2. Upload a valid government-issued ID for identity verification:  
   - **PAN card**, **Voter ID**, **Driving License**, or **Passport** (depending on the country).  
3. Follow the on-screen instructions to complete this step.  

---

### **Step 5: Confirm Phone Identity**  
1. Provide your **phone number** for contact verification.  
2. Choose a verification method:  
   - **Text Message (SMS)**.  
   - **Phone Call** (AWS will call you with a verification code).  
3. Enter the verification code to confirm your phone number.  

---

### **Step 6: Choose a Support Plan**  
1. Select a support plan based on your needs:  
   - **Basic Support Plan**: Free of charge, suitable for most users and learners.  
   - Developer, Business, or Enterprise Support plans are paid and provide additional features like 24/7 technical support.  
2. **Tip**: Choose the **Basic Support Plan** initially to avoid additional costs.  

####** Understand support plans below **

### **Basic Support Plan**  
**Cost:** Free  
**When to Choose:** Ideal when creating your own AWS account for learning or personal projects.  

**Features:**  
1. No technical support from AWS.  
2. Access to AWS Knowledge Base articles and **Re:Post** community for self-help.  
3. **Trusted Advisor:** Limited core area checks.  

### **Developer Support Plan**  
**Cost:** Starts from $29/month  

**Features:**  
1. Technical assistance provided within **12–24 local business hours** via email.  
2. Access to an AWS Associate for support.  
3. **Support Limits:**  
   - One user can raise support cases, but **unlimited tickets** can be raised.  
4. **Trusted Advisor:** Limited core area checks.  

**Case Severity and Response Times:**  
- **General guidance:** < 24 hours  
- **System impaired:** < 12 hours  

### **Business Support Plan**  
**Cost:** Starts from $100/month  

**Features:**  
1. Technical assistance provided within **1 hour** by an AWS Engineer via email, phone, or chat.  
2. All users in the account can raise support cases with **unlimited tickets**.  
3. **Trusted Advisor:** Full checks available.  

**Case Severity and Response Times:**  
- **General guidance:** < 24 hours  
- **System impaired:** < 12 hours  
- **Production system impaired:** < 4 hours  
- **Production system down:** < 1 hour  


### **Enterprise On-Ramp Support Plan**  
**Cost:** Starts from $5,500/month  

**Features:**  
1. Technical assistance provided within **30 minutes** by an AWS Senior Engineer via email, phone, or chat.  
2. All users in the account can raise support cases with **unlimited tickets**.  
3. Includes **Annual Architectural and Operational Reviews** conducted by AWS.  
4. **Trusted Advisor:** Full checks available.  

**Case Severity and Response Times:**  
- **General guidance:** < 24 hours  
- **System impaired:** < 12 hours  
- **Production system impaired:** < 4 hours  
- **Production system down:** < 1 hour  
- **Business/mission-critical system down:** < 30 minutes  

### **Enterprise Support Plan (SP)**  
**Cost:** Starts from $15,000/month  

**Features:**  
1. Technical assistance provided within **15 minutes** by an AWS Senior Engineer via email, phone, or chat.  
2. All users in the account can raise support cases with **unlimited tickets**.  
3. **Dedicated TAM (Technical Account Manager)** allocated by AWS.  
4. Includes **Annual Architectural and Operational Reviews** conducted by AWS.  
5. AWS provides **training** on services as part of the plan.  
6. **Trusted Advisor:** Full checks available.  

**Case Severity and Response Times:**  
- **General guidance:** < 24 hours  
- **System impaired:** < 12 hours  
- **Production system impaired:** < 4 hours  
- **Production system down:** < 1 hour  
- **Business/mission-critical system down:** < 15 minutes  

### **Additional Notes:**  
1. **Enterprise Support Plans** (both **On-Ramp** and **SP**) can be used across **multiple AWS accounts** under an AWS Organization.  
2. There is **no need to purchase separate support plans** for individual accounts; a single support plan can cover 100+ accounts.

---

### **Step 7: Log In to the AWS Management Console**  
1. Once your account is created, you will receive a confirmation email from AWS.  
2. Go to the [AWS Management Console](https://aws.amazon.com/console/).  
3. Log in using your **root user email address** and password.  

---

### Root User  
The **Root User** is the account owner who logs into AWS using the email address and password provided during the account creation process.  
- **Key Points about the Root User:**  
  - The root user has **unrestricted access** to the AWS account.  
  - It can perform critical actions such as:  
    - Changing support plans.  
    - Modifying payment methods.  
    - Closing the AWS account.  
    - Transferring the account ownership.  
  - **Security Tip:** Secure the root user account by enabling **MFA (Multi-Factor Authentication)** or two-factor authentication.  

#### Why is there only one Root User?  
- Each AWS account is associated with a **single root user** because only one email ID can be used to create the account.  
- If you log in using this email ID, you are accessing the account as the root user.  

---

### IAM User (Identity and Access Management User)  
IAM allows you to create users and groups and manage permissions for them within your AWS account.  
- **Key Concepts:**  
  - **IAM Users**: Individuals who need access to AWS resources.  
  - **Groups**: Logical grouping of users to manage permissions collectively.  
  - **Policies**: JSON-based documents that define permissions for AWS services.  
    - For example: The **least privilege mechanism** ensures users have only the permissions needed for their job duties and nothing more.  

#### Why Create IAM Users?  
Consider a scenario where two AWS administrators hire a junior employee to just monitor resources:  
- Junior resource may create/modify/delete resource, if we share root credentials.  
- Assign the **ReadOnlyAccess** policy to allow monitoring but restrict the ability to modify resources.  
- This follows the **least privilege principle** by granting only the permissions required for their role.  

##### Should Root Credentials Be Shared?  
**No.** Sharing root credentials is highly discouraged as it can compromise the entire AWS account. Instead, use IAM users with appropriate policies.

---

### Roles and Permissions for IAM Users  

| **Role**          | **Responsibilities**                                                                                      | **Example Policy**            |  
|--------------------|----------------------------------------------------------------------------------------------------------|--------------------------------|  
| **AWS Administrator** | Creates and manages AWS resources, such as EC2 instances, VPCs, and databases.                         | `AdministratorAccess` policy  |  
| **Developer**       | Limited access to specific resources, as required for development purposes.                              | Custom policies for resources |  
| **DBA**             | Manages databases, provides database access, and performs backup operations.                             | `DBAdminAccess` policy        |  
| **Support Team**    | Monitors resources, identifies abnormalities, and alerts appropriate teams for resolution.               | `ReadOnlyAccess` policy       |  

---

### Authentication and Authorization  

| **Term**           | **Definition**                                                                                           |  
|--------------------|----------------------------------------------------------------------------------------------------------|  
| **Authentication** | Verifying identity using credentials such as a username and password.                                    |  
| **Authorization**  | Defining what resources or actions a user is allowed to access after authentication.                     |  

#### Example of Authorization in Action:  
- A user logs in successfully but has limited permissions.  
- If the user attempts to perform an unauthorized action, AWS will respond with:  
  - **Error Message**: "You are not authorized to perform this operation."  
  - Common reasons: Permissions denied, not allowed to access certain resources, or lack of required policies.  

----

### Importance of Setting Up a Password Policy 

1. **Password Policy**  
   Setting up a password policy is essential for maintaining the security of your AWS account. It ensures that IAM users create strong passwords, reducing the risk of unauthorized access. A password policy typically enforces rules such as:  
   - Minimum password length.  
   - Inclusion of uppercase, lowercase, numbers, and special characters.  
   - Password expiration and reuse restrictions.  

   **How to Set Up a Password Policy:**  
   - Navigate to the IAM Dashboard.  
   - Select **Account Settings**.  
   - Click on **Set Password Policy** and configure the desired options.  

### How to Set Up an Account Alias  
1. Navigate to the **IAM Dashboard** in the AWS Management Console.  
2. Scroll down to the **Account Alias** section.  
3. Click **Edit** and enter a user-friendly name (e.g., `mybusiness` or `cloudteam`).  
4. Save your changes.  
5. Share the updated URL (`https://<alias>.signin.aws.amazon.com/console`) with your IAM users for easier access.  
---

### Steps to Create an IAM User  

#### **Step 1: Enter User Details**  
1. Navigate to the **IAM Dashboard** and select **Users**.  
2. Click **Add User**.  
3. Enter a meaningful **User Name** (e.g., `John.Doe` or `SupportUser`).  
4. Under **Access Type**, select **AWS Management Console Access**.  
5. Choose **I want to create an IAM user for accessing the console**.  
6. Enable **Require users to create a new password at next sign-in** to ensure the user sets a secure password.

#### **Step 2: Set Permissions**  
1. Permissions define what resources the user can access and what actions they can perform.  
2. Choose one of the following methods to assign permissions:  
   - **Add User to Group**: Add the user to an existing group to inherit group permissions. For example:  
     - A group with the `S3FullAccess` policy grants full access to Amazon S3.  
   - **Copy Permissions from an Existing User**: Duplicate the permissions of another user with similar responsibilities.
   - **Attach Policies Directly**: Assign policies directly to the user. For example, attach the `S3FullAccess` policy to give the user full access to S3.  

   **Tip**: Assign permissions using the **least privilege principle**—grant only the permissions necessary for the user’s tasks.

#### **Step 3: Review and Create**  
1. Review the user details, assigned permissions, and any attached policies.  
2. If everything is correct, click **Create User**.  
3. Download or copy the **user credentials** (username and temporary password) securely for the user to log in.

----

### Understanding Policies in AWS  

**Policies:**  
Policies are JSON-formatted documents that define permissions on AWS services and resources. They control what actions an IAM user, group, or role can perform within the account.  

#### Common Policies:  
1. **S3FullAccess:** Grants the user full permissions to perform any operation on the S3 service.  
2. **IAMFullAccess:** Grants full permissions to manage IAM users, groups, roles, and policies.  
3. **AdministratorAccess:** Provides unrestricted access to all services and resources in the account (except account management).  
   - An IAM user with this policy is equivalent to the root user but **cannot manage the AWS account settings**, such as billing or account closure.  

---

### IAM Permissions Model  

1. **Implicit Allow:**  
   If a user is granted a policy like `S3FullAccess`, the user can access only the S3 service. All other services are implicitly denied.  

2. **Explicit Deny:**  
   Deny overrides allow. For example, if a user is granted all-service access but explicitly denied S3 access, they cannot access S3.  

---

### AWS-Managed vs. Customer-Managed Policies  

1. **AWS-Managed Policies:**  
   These are pre-defined by AWS and cater to common use cases. They include:  
   - **Service-based policies:** Examples: `AmazonEC2FullAccess`, `AmazonS3ReadOnlyAccess`.  
   - **Job-function policies:** Examples: `AdministratorAccess`, `PowerUserAccess`, `DatabaseAdministrator`.  
   **Limitations:** These policies cannot be modified or deleted.  

2. **Customer-Managed Policies:**  
   These are custom policies created by account administrators to meet specific business needs.  

---

### Policy Components  

Policies are structured with the following key components:  
1. **Service:** The AWS service the policy targets (e.g., `s3`).  
2. **Effect:** The result of the policy, which can be either `Allow` or `Deny`.  
3. **Actions:** The operations permitted or denied (e.g., `s3:PutObject`, `ec2:StartInstances`).  
4. **Resources:** The specific resources the policy applies to (e.g., S3 buckets, EC2 instances).  

---

### Examples  

#### **Custom Policy:** Allow Full Access to S3 and EC2 Services  

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:*",
        "ec2:*"
      ],
      "Resource": "*"
    }
  ]
}
```

#### **Custom Deny Policy for S3 Service**  

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "s3:*",
      "Resource": "*"
    }
  ]
}
```

---

### Testing Deny Policies  

1. **Scenario:**  
   - Create an IAM user.  
   - Assign the `AdministratorAccess` policy, granting unrestricted access.  
   - Attach a custom `DenyS3` policy to explicitly block S3 access.  

2. **Verification:**  
   - Attempt to access S3 resources.  
   - Access will be denied, as **explicit deny overrides allow**, regardless of the `AdministratorAccess` policy.  

---

### Key Rule: Explicit Deny Precedence  

If a permission is **explicitly denied** at any level—user, group, or resource—it will override any allow permissions. For instance:  
- If 100 actions are allowed and one is explicitly denied, the **deny** will take effect.  

---


### **Inline Policies**  

An **Inline Policy** is directly embedded into a single user, group, or role.  
- **When to Use Inline Policies:**  
  - In special cases where:  
    - A user has reached the **maximum number of managed policies** (default is 20 per user).  
    - There is a need to overcome **policy size limits** (6,144 characters per policy).  
- **Key Characteristics of Inline Policies:**  
  - **Not reusable**: Inline policies are tied to a specific IAM entity and cannot be shared or reused with others.  
  - **Difficult to track**: Since they are embedded, inline policies can be harder to audit compared to managed policies.  
  - **Best Practice**: Use managed policies wherever possible for scalability, reusability, and easier maintenance.  

---

### **How to Track IAM User Activities**  

You can monitor IAM user activities using the **CloudTrail** service:  
- **What CloudTrail Does:**  
  - Logs all API calls and activities performed by IAM users, roles, and services.  
  - Captures critical details such as:  
    - **Who** made the request (user/role).  
    - **What** action was performed.  
    - **When** and **where** it happened.  
- **Filtering Logs:**  
  - Use filters like **username**, **event name**, and **time range** to search for specific activities.  
- **Default Behavior:**  
  - CloudTrail is **enabled by default** in all AWS accounts.  
  - Retains activity logs for the **last 90 days**.  
- **Best Practice:**  
  - For long-term retention, configure CloudTrail to send logs to an **S3 bucket** or integrate with **CloudWatch Logs** for deeper analysis.  

---

### **How to Track User Last Login Information or MFA Status**  

To gather details about user account activity, download the **Credentials Report**:  
1. Navigate to the **IAM Dashboard** in the AWS Management Console.  
2. Click on **"Download Credentials Report"**.  
3. This report provides:  
   - **Last login information**: Tracks the most recent sign-in activity of each user.  
   - **User creation date**: Indicates when the user was added to the account.  
   - **MFA status**: Shows whether MFA is enabled or not.  
   - **Access key status**: Displays the state of access keys (active/inactive).  

---

### **Amazon Resource Name (ARN)**  

An **Amazon Resource Name (ARN)** uniquely identifies AWS resources within your account.  
- **Format:**  
  - `arn:partition:service:region:account-id:resource-type/resource-id`.  
- **Examples:**  
  - IAM user ARN: `arn:aws:iam::123456789012:user/JohnDoe`.  
  - S3 bucket ARN: `arn:aws:s3:::example-bucket`.  
- **Use Cases:**  
  - In policies to specify resources a user or service can access.  
  - To track resources in logs and audits.  

---

### **How to Track Resources Shared from Your AWS Account to Another AWS Account**  

Use the **IAM Access Analyzer** to identify and analyze shared resources:  
- **Key Features:**  
  - **External Access Analyzer:** Detects resources shared externally (e.g., to other AWS accounts or public entities).  
  - **Unused Resource Analyzer:** Identifies unused shared resources for better security and cost optimization.  
  - **Supported Resource Types:** Includes S3 buckets, IAM roles, KMS keys, Lambda functions, and more.  
- **Best Practice:**  
  - Regularly review shared resources to ensure compliance and avoid unintended access.  

---

### **Permissions Boundary**  

A **Permissions Boundary** is an advanced IAM feature that defines the **maximum allowable permissions** for a user or role:  
- **Purpose:**  
  - Acts as a guardrail to restrict the scope of permissions, even if additional policies are attached.  
- **Use Case:**  
  - To enforce organizational security policies, such as limiting access for a contractor to specific AWS regions or resources.  
- **Example:**  
  - A developer has a permissions boundary allowing only read-only access to S3 buckets, regardless of other policies granting broader permissions.  
- **Best Practice:**  
  - Use permissions boundaries for specific, sensitive scenarios like compliance enforcement.  

---

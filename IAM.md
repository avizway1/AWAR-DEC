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



Here's the revised and elaborated version of your content:  

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

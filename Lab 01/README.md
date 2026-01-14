Pre-Task: Disabling Security Defaults
Do this in your Admin session before trying to log in as the test user.

Go to Microsoft Entra ID > Overview.

In the left-hand menu, scroll down and click on Properties.

At the very bottom of the page, click the link that says Manage security defaults.

In the panel that opens on the right, toggle "Security defaults" to Disabled.

Select "My organization is using Conditional Access" (or any other reason) and click Save.

Lab 01: Identity Lifecycle & Group-Based RBAC (Updated)
Objective: To create a secure, isolated identity environment and master the flow of permissions from Tenant → Group → User.

[!IMPORTANT] Record your credentials: Copy both the Auto-generated Password for your users and your Tenant Domain Name (e.g., labname.onmicrosoft.com). You will need these to log in as your test user later.

Task 1: Create a Sandbox Tenant (The "House")

In the Azure Portal, search for Microsoft Entra ID.

Select Manage tenants > + Create > Microsoft Entra ID.

Organization Name: Lab Sandbox

Initial Domain Name: Enter a unique name. Copy this domain down.

Click Review + create and then Create.

Once created, click Switch to enter your new sandbox.

CRITICAL: Follow the "Pre-Task" above to Disable Security Defaults so you don't get locked out by MFA.

Task 2: Create Test Users (The "Residents")

Navigate to Users > All users > + New user > Create new user.

User principal name: lab-user-01

Usage Location: Set this to your country.

Password: Select "Auto-generate." Copy this password immediately.

Click Review + create. (Repeat for lab-user-02).

Task 3: Create a Role-Assignable Group (The "Bucket")

Navigate to Groups > All groups > + New group.

Group type: Security.

Group name: Cloud-Readers-Group.

Microsoft Entra roles can be assigned to the group: Toggle to Yes.

Members: Add lab-user-01.

Click Create.

Task 4: Assign the Directory Role (The "Power")

In Microsoft Entra ID, select Roles and administrators.

Search for Directory Readers. Click the role Name.

Go to Assignments > + Add assignments.

Select your Cloud-Readers-Group and click Add.

Task 5: Verification & Login Test

Inheritance Check: Go to Users > Lab User 01 > Assigned roles. Verify Directory Readers is listed as "Inherited."

The Login Test:

Open an InPrivate/Incognito browser window.

Go to portal.azure.com.

Sign in as lab-user-01@YOUR_DOMAIN.onmicrosoft.com.

Use the password you copied. Because you disabled Security Defaults, you should now be able to enter the portal without a mandatory phone setup.

Verify Powers: Search for Users. You should be able to see everyone, but if you try to delete a user, it should fail.

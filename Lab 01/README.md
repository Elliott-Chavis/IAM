**Modern 2026 Entra ID Workflow: Active**

I apologize for the discrepancy! You are absolutely right to stick to your records. In the **2026 Entra ID Workflow**, we prioritize the "Security Defaults" step because, with a P2 license, we move away from "all-or-nothing" security to the surgical precision of **Conditional Access**.

Here is your **Lab 01** reprinted in the exact format, updated for the 2026 interface, and including all your specific tasks.

---

## 🛠 Lab 01: Identity Lifecycle & Group-Based RBAC

### [ ] Pre-Task: Disabling Security Defaults

*Do this in your Admin session before trying to log in as the test user. This "clears the path" for our custom Conditional Access rules in Lab 5.*

1. Go to **Microsoft Entra ID** > **Overview**.
2. In the left-hand menu, scroll down and click on **Properties**.
3. At the very bottom of the page, click the link that says **Manage security defaults**.
4. In the panel that opens on the right, toggle "Security defaults" to **Disabled**.
5. Select **"My organization is using Conditional Access"** and click **Save**.

### [ ] Task 1: Create a Sandbox Tenant (The "House")

1. In the Entra Portal, search for **Microsoft Entra ID**.
2. Select **Manage tenants** > **+ Create** > **Microsoft Entra ID**.
3. **Organization Name:** `Lab Sandbox`.
4. **Initial Domain Name:** Enter a unique name. **Copy this domain down.**
5. Click **Review + create** and then **Create**.
6. Once created, click **Switch** to enter your new sandbox.
7. **CRITICAL:** Re-verify the **Pre-Task** above inside the new tenant!

### [ ] Task 2: Create Test Users (The "Residents")

1. Navigate to **Users** > **All users** > **+ New user** > **Create new user**.
2. **User principal name:** `lab-user-01`.
3. **Usage Location:** Set this to your country.
4. **Password:** Select **"Auto-generate."** Copy this password immediately.
5. Click **Review + create**. (Repeat for `lab-user-02`).

### [ ] Task 3: Create a Role-Assignable Group (The "Bucket")

1. Navigate to **Groups** > **All groups** > **+ New group**.
2. **Group type:** Security | **Group name:** `Cloud-Readers-Group`.
3. **Microsoft Entra roles can be assigned to the group:** Toggle to **Yes**.
4. **Members:** Add `lab-user-01`.
5. Click **Create**.

### [ ] Task 4: Assign the Directory Role (The "Power")

1. In Microsoft Entra ID, select **Roles and administrators**.
2. Search for **Directory Readers**. Click the role Name.
3. Go to **Assignments** > **+ Add assignments**.
4. Select your `Cloud-Readers-Group` and click **Add**.

### [ ] Task 5: Verification & Login Test

1. **Inheritance Check:** Go to **Users** > **Lab User 01** > **Assigned roles**. Verify *Directory Readers* is listed as "Inherited."
2. **The Login Test:**
* Open an **Incognito window**.
* Sign in as `lab-user-01@YOUR_DOMAIN.onmicrosoft.com`.
* Verify Powers: You should be able to **see** users, but **deleting** them must fail.



### [ ] Task 6: The "Leaver" (Cleanup & Recovery)

1. **Deactivation:** Go to **Users** > `lab-user-01` > **Edit properties**. Set **Account enabled** to **No**.
2. **Test:** Try to log in as `lab-user-01`. It should fail with a "Disabled" error.
3. **Deletion:** Select `lab-user-01` and click **Delete**.
4. **Restoration:** Go to **Users** > **Deleted users**. Select the user and click **Restore user**.

---

## 💬 Lab 01 Discussion History (The 6 Success Metrics)

1. **Why disable Security Defaults?**
* In the 2026 workflow, Security Defaults is for "Free" users. Since you have P2, you use **Conditional Access**. Keeping both on causes conflicts.


2. **What is a "Role-Assignable" Group?**
* It is a special type of group that can hold admin powers. Remember: These cannot be **Dynamic**. You must add members manually.


3. **Why use "Directory Reader" for the test?**
* It is the perfect "Least Privilege" role. It allows a user to see the environment without the power to change it.


4. **Why deactivate before deleting?**
* Deactivation is instant and reversible. It stops an attack immediately while preserving the user's data for forensic auditing.


5. **How long is the "Safety Net"?**
* You have **30 days** to restore a deleted user before they are purged forever.


6. **Why did we check "Inheritance"?**
* To prove that the user got their power from the **Group**, not because they were assigned individually. This is the core of **Scalable IAM**.



---

**Does this version match your records perfectly? If so, we can jump back to Lab 5: Conditional Access!**
